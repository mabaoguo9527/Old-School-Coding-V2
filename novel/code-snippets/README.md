# 全书代码片段预设库

**Purpose**: 预写全书关键代码片段，确保技术准确性和一致性。创作时直接引用。

---

## 使用说明

1. 每段代码都标注了适用章节、技术点和准确性说明
2. 代码以Java为主，遵循JDK 17 LTS标准
3. 核心逻辑MUST可编译通过（允许省略import）
4. 创作时可根据叙事需要截取部分代码，但不可修改核心逻辑

---

## 卷一代码片段

### CS-001: volatile + CAS 线程模型（第3章·白板手写）

**场景**：马农在白板上手写Java线程模型，讲解内存可见性

```java
// 马农白板手写：volatile保证可见性
private volatile boolean running = true;
private volatile int counter = 0;

// CAS操作——以巧取胜的无锁之锁
public void increment() {
    int current;
    do {
        current = counter;  // 读取当前值
    } while (!compareAndSwap(counter, current, current + 1));
    // 不排队，反复试探，得手即走
}
```

**准确性**：`volatile`关键字在JDK 17中确保happens-before关系。CAS操作通过`Unsafe.compareAndSwapInt`实现（JDK 9+推荐`VarHandle`）。白板手写场景中使用伪代码形式的CAS是合理的。

---

### CS-002: ClassLoader热加载补丁（第4章·堆区倒计时）

**场景**：JVM堆区耗尽前30秒，马农手写ClassLoader热加载

```java
// 紧急热加载——在不重启JVM的情况下替换核心类
public class HotPatchLoader extends ClassLoader {
    
    @Override
    protected Class<?> findClass(String name) throws ClassNotFoundException {
        byte[] classData = loadPatchBytes(name);  // 从本地磁盘读取补丁
        if (classData != null) {
            return defineClass(name, classData, 0, classData.length);
        }
        throw new ClassNotFoundException(name);
    }
    
    // 绕过双亲委派——直接加载补丁版本
    @Override
    public Class<?> loadClass(String name) throws ClassNotFoundException {
        if (name.startsWith("com.tencent.core.")) {
            return findClass(name);  // 核心包直接走补丁
        }
        return super.loadClass(name);  // 其他包走正常委派
    }
}
```

**准确性**：自定义ClassLoader + 覆写`loadClass`绕过双亲委派是JDK标准用法。`defineClass`接收字节数组定义类。生产环境中Arthas/JRebel等工具的底层原理类似。

---

### CS-003: G1 GC参数止血（第12章·走火入魔）

**场景**：堆区暴涨如真气逆行，马农手写G1 GC参数

```bash
# G1 GC调优——疏通经络
# 1. 限制GC停顿时间
-XX:MaxGCPauseMillis=200
# 2. 调整Region大小（堆区32GB时建议16MB）
-XX:G1HeapRegionSize=16m
# 3. 提高并发标记线程数
-XX:ConcGCThreads=8
# 4. 降低触发Mixed GC的阈值——更早开始回收
-XX:InitiatingHeapOccupancyPercent=35
# 5. 禁用显式GC调用（防止Origin残留代码触发Full GC）
-XX:+DisableExplicitGC
```

**准确性**：全部为HotSpot VM真实支持的JVM参数。G1 GC是JDK 17的默认垃圾回收器。`InitiatingHeapOccupancyPercent`默认45%，降到35%会更早触发并发标记。

---

### CS-004: vi手写Java应急服务（第13章·手术刀与铁锤）

**场景**：马农在vi中手写200行Java应急路由服务核心片段

```java
// 应急路由服务——接管核心流量分发
public class EmergencyRouter {
    
    private final Map<String, ServerSocket> routes = new ConcurrentHashMap<>();
    private final ExecutorService pool = Executors.newFixedThreadPool(
        Runtime.getRuntime().availableProcessors() * 2
    );
    
    public void start(int port) throws IOException {
        ServerSocket server = new ServerSocket(port);
        System.out.println("[EmergencyRouter] Listening on port " + port);
        
        while (true) {
            Socket client = server.accept();
            pool.submit(() -> handleRequest(client));
        }
    }
    
    private void handleRequest(Socket client) {
        try (var in = new BufferedReader(new InputStreamReader(client.getInputStream()));
             var out = new PrintWriter(client.getOutputStream(), true)) {
            
            String request = in.readLine();
            String response = route(request);
            out.println(response);
            
        } catch (IOException e) {
            // 静默处理——应急模式下不能因为异常停服
        }
    }
}
```

**准确性**：标准Java NIO + 线程池模型。`ConcurrentHashMap`是线程安全的路由表。`try-with-resources`是JDK 7+语法。线程池大小`CPU核数*2`是IO密集型场景的常见配置。

---

### CS-005: CAS无锁计数器（第18章·以一敌万）

**场景**：高并发洪峰下的CAS无锁编程

```java
// CAS无锁计数器——不排队、反复试探、得手即走
import java.util.concurrent.atomic.AtomicLong;
import java.util.concurrent.atomic.LongAdder;

public class HighConcurrencyCounter {
    
    // 方案一：AtomicLong（CAS自旋）
    private final AtomicLong atomicCount = new AtomicLong(0);
    
    // 方案二：LongAdder（分段CAS，千军万马分道走）
    private final LongAdder adderCount = new LongAdder();
    
    // 低并发用AtomicLong，高并发用LongAdder
    public void increment(boolean highConcurrency) {
        if (highConcurrency) {
            adderCount.increment();  // 分段竞争，吞吐量更高
        } else {
            atomicCount.incrementAndGet();  // 单点CAS，延迟更低
        }
    }
}
```

**准确性**：`AtomicLong`和`LongAdder`均为JDK标准类。`LongAdder`在JDK 8引入，内部使用`Cell[]`分段减少竞争，适用于高并发写场景。

---

### CS-006: CAS ABA问题（第30章·ABA陷阱）

**场景**：教学场景，讲解CAS的ABA问题

```java
// ABA问题演示——狸猫换太子
// 值虽然回来了，但它已经不是原来那个值
AtomicStampedReference<Integer> ref = 
    new AtomicStampedReference<>(100, 0);  // 值=100, 版本=0

// 线程A读取
int[] stampHolder = new int[1];
Integer value = ref.get(stampHolder);  // value=100, stamp=0

// 线程B: 100→200→100（ABA！）
ref.compareAndSet(100, 200, 0, 1);  // 100→200, stamp: 0→1
ref.compareAndSet(200, 100, 1, 2);  // 200→100, stamp: 1→2

// 线程A尝试CAS: 失败！因为stamp不匹配（期望0，实际2）
boolean success = ref.compareAndSet(100, 300, 0, 3);  // false
// 版本号就是防伪标签——值相同但版本不同，说明被动过
```

**准确性**：`AtomicStampedReference`是JDK标准解决ABA问题的方案，通过版本号（stamp）区分"看起来相同但实际被修改过"的情况。

---

### CS-007: @Contended伪共享修复（第31章·伪共享之毒）

**场景**：CPU缓存行伪共享问题排查和修复

```java
// 伪共享问题——CPU缓存行的暗毒
// 两个线程分别修改counter1和counter2
// 如果它们在同一个缓存行（64字节），每次修改都会导致对方缓存失效

// 修复前：两个long（共16字节）在同一缓存行
class BadCounter {
    volatile long counter1;  // 线程A修改
    volatile long counter2;  // 线程B修改——但会被A的修改"牵连"
}

// 修复后：@Contended让JVM自动填充，隔离到不同缓存行
@jdk.internal.misc.Contended  // JDK 8+
class GoodCounter {
    volatile long counter1;
    volatile long counter2;  // 现在各自独立，互不干扰
}
// 运行时需要: -XX:-RestrictContended
```

**准确性**：`@Contended`注解在`jdk.internal.misc`包下，用于消除伪共享（false sharing）。需要JVM参数`-XX:-RestrictContended`才能生效。`LongAdder`内部的`Cell`类就使用了此注解。

---

## 卷一·第四幕代码片段

### CS-008: ARM心跳监测（第39章·心跳协议）

**场景**：手写嵌入式心跳监测程序

```c
// 心跳监测——每行代码关乎人命
// ARM Cortex-M4, 裸机C
#define SENSOR_ADDR  0x40010000
#define ALARM_PIN    GPIO_PIN_5

volatile uint32_t* sensor_reg = (volatile uint32_t*)SENSOR_ADDR;
volatile uint32_t heartbeat_count = 0;

void SysTick_Handler(void) {  // 每10ms触发一次
    uint32_t reading = *sensor_reg;
    
    if (reading > THRESHOLD_HIGH || reading < THRESHOLD_LOW) {
        heartbeat_count++;
        if (heartbeat_count >= 3) {  // 连续3次异常才报警
            HAL_GPIO_WritePin(GPIOA, ALARM_PIN, GPIO_PIN_SET);
        }
    } else {
        heartbeat_count = 0;  // 正常则重置计数
    }
}
```

**准确性**：`SysTick_Handler`是ARM Cortex-M系列标准中断服务例程。`HAL_GPIO_WritePin`是STM32 HAL库的真实API。内存映射IO通过`volatile`指针访问是嵌入式标准做法。

---

### CS-009: G1 GC STW调优（第44章·GC停顿风暴）

**场景**：G1 GC Stop-The-World长达10秒

```bash
# 诊断：GC日志分析
-Xlog:gc*:file=gc.log:time,uptime,level,tags

# 发现：Mixed GC频率过低，Old Region堆积导致Full GC
# [GC pause (G1 Evacuation Pause) (mixed), 10.234 secs]

# 修复：更激进的Mixed GC策略
-XX:G1MixedGCCountTarget=4        # 减少Mixed GC轮次
-XX:G1MixedGCLiveThresholdPercent=65  # 降低存活对象阈值
-XX:MaxGCPauseMillis=100           # 从200降到100
-XX:G1HeapWastePercent=5           # 降低可容忍的堆浪费
```

**准确性**：全部为HotSpot G1 GC真实参数。`G1MixedGCCountTarget`控制Mixed GC的目标轮次数。GC日志格式使用JDK 17+的`-Xlog`统一日志框架。

---

## 后续卷预留位（创作时补充）

### 卷二预留
- CS-010: 有限状态机（第53章）
- CS-011: Netty路由重写（第76-80章）
- CS-012: Spring Boot自动装配（第86-90章）
- CS-013: 熔断器模式（第91-95章）
- CS-014: 手写MQ（第106-110章）
- CS-015: JWT认证（第106-110章）
- CS-016: 字节码对决（第126-130章）

### 卷三预留
- CS-017: 服务网格/链路追踪（第151-155章）
- CS-018: JVM极致调优（第181-190章）
- CS-019: 密码学攻防（第191-200章）
- CS-020: CompletableFuture异步编排（第241-250章）
- CS-021: 内存屏障/x86 mfence（第251-260章）

### 卷四预留
- CS-022: 全球DNS手写启动（第296-300章）
- CS-023: x86汇编引导程序（第286-295章）
