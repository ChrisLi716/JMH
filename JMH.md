JMH  Java Microbenchmark Harness

如何在项目中引用 JMH

![image-20230819160823114](C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20230819160823114.png)



> https://github.com/openjdk/jmh.git

```java
org.openjdk.jmh.samples.JMHSample_01_HelloWorld#main
    
# JMH version: 1.38-SNAPSHOT   -- JMH版本号
# VM version: JDK 1.8.0_361, Java HotSpot(TM) 64-Bit Server VM, 25.361-b09
# VM invoker: C:\Program Files\Java\jdk1.8.0_361\jre\bin\java.exe
# VM options: -javaagent:C:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\lib\idea_rt.jar=63119:C:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\bin -Dfile.encoding=UTF-8
# Blackhole mode: full + dont-inline hint (auto-detected, use -Djmh.blackhole.autoDetect=false to disable) -- 黑洞模式
# Warmup: 5 iterations, 10 s each       -- 测试前对测试对象进行5轮预热，每次执行10秒
# Measurement: 5 iterations, 10 s each  -- 真正时对测试对象进行5轮测试，每次执行10秒
# Timeout: 10 min per iteration
# Threads: 1 thread, will synchronize iterations  -- 默认只会在一个线程里面执行测试
# Benchmark mode: Throughput, ops/time		      -- 将输出结果打印成 Throughput【吞吐量】的模式来看输出结果
# Benchmark: org.openjdk.jmh.samples.JMHSample_01_HelloWorld.wellHelloThere  -- 此类中标识了 @Benchmark 的测试对象

# Run progress: 0.00% complete, ETA 00:01:40
# Fork: 1 of 1
# Warmup Iteration   1: 3760163825.594 ops/s   -- 一轮跑了10秒，每秒跑 3760163825.594 次
# Warmup Iteration   2: 4430889451.652 ops/s
# Warmup Iteration   3: 4439455072.862 ops/s
# Warmup Iteration   4: 4409147073.419 ops/s
# Warmup Iteration   5: 4409733220.347 ops/s
Iteration   1: 4389189990.659 ops/s
Iteration   2: 4437504114.906 ops/s
Iteration   3: 4413845865.828 ops/s
Iteration   4: 4401591543.047 ops/s
Iteration   5: 4432448561.087 ops/s


Result "org.openjdk.jmh.samples.JMHSample_01_HelloWorld.wellHelloThere":
  4414916015.106 ±(99.9%) 78399326.229 ops/s [Average]
  (min, avg, max) = (4389189990.659, 4414916015.106, 4437504114.906), stdev = 20360056.054  -- 最小值，平均值，最大值，标准差
  CI (99.9%): [4336516688.876, 4493315341.335] (assumes normal distribution) -- 围住区间

# Run complete. Total time: 00:01:40

REMEMBER: The numbers below are just data. To gain reusable insights, you need to follow up on
why the numbers are the way they are. Use profilers (see -prof, -lprof), design factorial
experiments, perform baseline and negative tests that provide experimental control, make sure
the benchmarking environment is safe on JVM/OS/HW level, ask for reviews from the domain experts.
Do not assume the numbers tell you what you want them to tell.

Benchmark                                Mode  Cnt           Score          Error  Units
JMHSample_01_HelloWorld.wellHelloThere  thrpt    5  4414916015.106 ± 78399326.229  ops/s 

Process finished with exit code 0
```



```java
@Warmup(iterations = 1, time = 1) // 预热次数和时间
@Measurement(iterations = 1, time = 1) // 测试次数和时间
public class JMHSample_01_HelloWorld{
...
}
# JMH version: 1.38-SNAPSHOT
# VM version: JDK 1.8.0_361, Java HotSpot(TM) 64-Bit Server VM, 25.361-b09
# VM invoker: C:\Program Files\Java\jdk1.8.0_361\jre\bin\java.exe
# VM options: -javaagent:C:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\lib\idea_rt.jar=49219:C:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\bin -Dfile.encoding=UTF-8
# Blackhole mode: full + dont-inline hint (auto-detected, use -Djmh.blackhole.autoDetect=false to disable)
# Warmup: 1 iterations, 1 s each
# Measurement: 1 iterations, 1 s each
# Timeout: 10 min per iteration
# Threads: 1 thread, will synchronize iterations
# Benchmark mode: Throughput, ops/time
# Benchmark: org.openjdk.jmh.samples.JMHSample_01_HelloWorld.wellHelloThere

# Run progress: 0.00% complete, ETA 00:00:02
# Fork: 1 of 1
# Warmup Iteration   1: 3655058565.766 ops/s
Iteration   1: 3803946570.160 ops/s


Result "org.openjdk.jmh.samples.JMHSample_01_HelloWorld.wellHelloThere":
  3803946570.160 ops/s


# Run complete. Total time: 00:00:02

REMEMBER: The numbers below are just data. To gain reusable insights, you need to follow up on
why the numbers are the way they are. Use profilers (see -prof, -lprof), design factorial
experiments, perform baseline and negative tests that provide experimental control, make sure
the benchmarking environment is safe on JVM/OS/HW level, ask for reviews from the domain experts.
Do not assume the numbers tell you what you want them to tell.

Benchmark                                Mode  Cnt           Score   Error  Units
JMHSample_01_HelloWorld.wellHelloThere  thrpt       3803946570.160          ops/s

Process finished with exit code 0
```



## @BenchmarkMode 

### Throughput  吞吐量

```java
@Benchmark
@BenchmarkMode(Mode.Throughput)
@OutputTimeUnit(TimeUnit.SECONDS)
public void measureThroughput() throws InterruptedException {
	TimeUnit.MILLISECONDS.sleep(100);
}

Benchmark                                       Mode  Cnt  Score   Error  Units
JMHSample_02_BenchmarkModes.measureThroughput  thrpt    5  9.201 ± 0.031  ops/s  -- ops/s表示每秒多少次操作
```

### AverageTime  平均时间

```java
@Benchmark
@BenchmarkMode(Mode.AverageTime)
@OutputTimeUnit(TimeUnit.MICROSECONDS)
public void measureAvgTime() throws InterruptedException {
	TimeUnit.MILLISECONDS.sleep(100);
}

Benchmark                                   Mode  Cnt       Score     Error  Units
JMHSample_02_BenchmarkModes.measureAvgTime  avgt    5  108758.884 ± 494.750  us/op --us/op 表示一次操作耗时多
 
@Benchmark
@BenchmarkMode(Mode.AverageTime)
@OutputTimeUnit(TimeUnit.SECONDS)
public void measureAvgTime() throws InterruptedException {
	TimeUnit.MILLISECONDS.sleep(100);
}    
Benchmark                                   Mode  Cnt  Score   Error  Units
JMHSample_02_BenchmarkModes.measureAvgTime  avgt       0.108           s/op    
```

### SampleTime 抽样

> 和 AverageTime  一样表示的是每次操作需要消耗多少秒
>
> 通过抽样可以直观感受到耗时的波动和算法的稳定性， 如果稳定性不高，随着抽样的增加耗时会出现比较大的波动
>
> 只是进行采样比对来统计耗时，不像吞吐量和平均值测试将每次运行都计算在内。

```java
@Benchmark
@BenchmarkMode(Mode.SampleTime)
@OutputTimeUnit(TimeUnit.SECONDS)
public void measureSamples() throws InterruptedException {
    TimeUnit.MILLISECONDS.sleep(100);
}

Benchmark                                             Mode  Cnt  Score   Error  Units
JMHSample_02_BenchmarkModes.measureSamples          sample   10  0.108 ± 0.003   s/op
JMHSample_02_BenchmarkModes.measureSamples:p0.00    sample       0.103           s/op -- 最少耗时
JMHSample_02_BenchmarkModes.measureSamples:p0.50    sample       0.108           s/op -- 50% 的操作是在0.108s内完成
JMHSample_02_BenchmarkModes.measureSamples:p0.90    sample       0.110           s/op
JMHSample_02_BenchmarkModes.measureSamples:p0.95    sample       0.110           s/op
JMHSample_02_BenchmarkModes.measureSamples:p0.99    sample       0.110           s/op -- 99% 的操作是在0.11s内完成
JMHSample_02_BenchmarkModes.measureSamples:p0.999   sample       0.110           s/op -- 99.9% 的操作是在0.11s内完成
JMHSample_02_BenchmarkModes.measureSamples:p0.9999  sample       0.110           s/op -- 99.99% 的操作是在0.11s内完成
JMHSample_02_BenchmarkModes.measureSamples:p1.00    sample       0.110           s/op -- 所有操作在 0.11s内完成
```



### SingleShotTime  单次执行耗时

> 1. 冷启动测试，此方法在JMH一轮测试中只会执行一次，这个模式主要是为了测试冷启动的性能
>
> 2. 云原生时代，Java是落后后其它语言的，因为java有一个预热的过程，java代码是越执行越快，它通过JIT的方式会让自己的执行效率越来越高, 而其它语言，比如GO语言，编译完后就已经最高执行效率的机器码
>
>    所以对于java代码来说，如何提高自己的冷启动的效率也是一个比较重要优化项

```java
@Benchmark
@BenchmarkMode(Mode.SingleShotTime)
@OutputTimeUnit(TimeUnit.MICROSECONDS)
public void measureSingleShot() throws InterruptedException {
	TimeUnit.MILLISECONDS.sleep(100);
}
Benchmark                                      Mode  Cnt       Score   Error  Units
JMHSample_02_BenchmarkModes.measureSingleShot    ss       102272.200          us/op
```



### Mode.All 全部测试

```java
@BenchmarkMode(Mode.All) 
等同于
@BenchmarkMode({Mode.Throughput, Mode.AverageTime, Mode.SampleTime, Mode.SingleShotTime})    
```



```java
@Benchmark
@BenchmarkMode({Mode.Throughput, Mode.AverageTime, Mode.SampleTime, Mode.SingleShotTime})
@OutputTimeUnit(TimeUnit.MICROSECONDS)
public void measureMultiple() throws InterruptedException {
	TimeUnit.MILLISECONDS.sleep(100);
}

Benchmark                                              Mode  Cnt       Score      Error   Units
JMHSample_02_BenchmarkModes.measureMultiple           thrpt           ≈ 10⁻⁵             ops/us -- 吞吐量测试
JMHSample_02_BenchmarkModes.measureMultiple            avgt       107870.110              us/op -- 平均值测试
JMHSample_02_BenchmarkModes.measureMultiple          sample   10  109169.869 ± 2678.978   us/op -- 抽样测试
JMHSample_02_BenchmarkModes.measureMultiple:p0.00    sample       107610.112              us/op
JMHSample_02_BenchmarkModes.measureMultiple:p0.50    sample       108724.224              us/op
JMHSample_02_BenchmarkModes.measureMultiple:p0.90    sample       113390.387              us/op
JMHSample_02_BenchmarkModes.measureMultiple:p0.95    sample       113770.496              us/op
JMHSample_02_BenchmarkModes.measureMultiple:p0.99    sample       113770.496              us/op
JMHSample_02_BenchmarkModes.measureMultiple:p0.999   sample       113770.496              us/op
JMHSample_02_BenchmarkModes.measureMultiple:p0.9999  sample       113770.496              us/op
JMHSample_02_BenchmarkModes.measureMultiple:p1.00    sample       113770.496              us/op
JMHSample_02_BenchmarkModes.measureMultiple              ss       101059.700              us/op	-- 冷启动测试
```



## @State



> @State 会标记在一个类上面，这个类会由JMH管理并初始化
>
> 在执行 @Benchmark 方法时会注入到方法中

### Scope

#### Scope.Thread

```java
// 这个静态内部类会在Benchmark各线程执行前初始化， 作为入参，且每个线程的入参都是不一样的
@State(Scope.Thread)
public static class ThreadState {
    volatile double x = Math.PI;
}

@Benchmark
public void measureUnshared(ThreadState state) {
    state.x++;
}
```



#### Scope.Beanchmark

```java
// 这个静态内部类会在整个Benchmark启动时初始化， 作为入参，且所有测试线程共享一个实例，用于测试有状态实例在多线程共享下的性能
@State(Scope.Benchmark)
public static class BenchmarkState {
	volatile double x = Math.PI;
}

@Benchmark
public void measureShared(BenchmarkState state) {
    state.x++;
}

```

```java
public static void main(String[] args) throws RunnerException {
    Options opt = new OptionsBuilder()
        .include(JMHSample_03_States.class.getSimpleName())
        .threads(4) // 在执行每一个benchmark时会创建4个线程
        .forks(1)
        .build();

    new Runner(opt).run();
}

Benchmark                             Mode  Cnt          Score   Error  Units
JMHSample_03_States.measureShared    thrpt        56734444.884          ops/s
JMHSample_03_States.measureUnshared  thrpt       569412894.729          ops/s
```



#### Scope.Group

> 当多个的benchmark标记为同一个组，标记为同一个组的benchmark会放在一起执行
>
> inc方法和get方法会被放到同一个benckmark里面去执行，并创建3个线程执行ink方法，创建一个线程执行get方法
>
> 如果需要测试一个方法在多线程下的执行效率时，可以使用@Group创造多线程下的竞争环境来衡量真实的执行效率



```java
@State(Scope.Group)
@BenchmarkMode(Mode.Throughput)
@OutputTimeUnit(TimeUnit.NANOSECONDS)
public class JMHSample_15_Asymmetric {

    private AtomicInteger counter;

    @Setup
    public void up() {
        counter = new AtomicInteger();
    }

    @Benchmark
    @Group("g")
    @GroupThreads(3) //启动3个线程去执行inc方法对变量counter进行自增
    public int inc() {
        return counter.incrementAndGet();
    }

    @Benchmark
    @Group("g")
    @GroupThreads(1) //启动一个线程去执行get方法获取counter里面的变量值
    public int get() {
        return counter.get();
    }


    @Benchmark
    @Group("g_single_get")
    public int single_get() {
        return counter.get();
    }


    @Benchmark
    @Group("g_single_ink_1")
    @GroupThreads(1)
    public int single_ink_1() {
        return counter.get();
    }

    @Benchmark
    @Group("g_single_ink_3")
    @GroupThreads(3)
    public int single_ink_3() {
        return counter.get();
    }

    public static void main(String[] args) throws RunnerException {
        Options opt = new OptionsBuilder()
                .include(JMHSample_15_Asymmetric.class.getSimpleName())
                .warmupIterations(1)
                .warmupTime(TimeValue.seconds(2))
                .measurementIterations(1)
                .measurementTime(TimeValue.seconds(1))
                .forks(1)
                .build();

        new Runner(opt).run();
    }
}
```

```java
Benchmark                                Mode  Cnt  Score   Error   Units
JMHSample_15_Asymmetric.g               thrpt       0.144          ops/ns
JMHSample_15_Asymmetric.g:get           thrpt       0.090          ops/ns
JMHSample_15_Asymmetric.g:inc           thrpt       0.054          ops/ns
JMHSample_15_Asymmetric.g_single_get    thrpt       0.721          ops/ns
JMHSample_15_Asymmetric.g_single_ink_1  thrpt       0.704          ops/ns
JMHSample_15_Asymmetric.g_single_ink_3  thrpt       1.940          ops/ns
```



### default state

```java
@State(Scope.Thread) // 相当于将当前类作为一个静态内部类，并在Benchmark各线程执行前初始化， 作为入参，且每个线程的入参都是不一样的, 这样会方便测试，不用声明一个类并将这个类作为参数传入Benchmark方法中
public class JMHSample_04_DefaultState{
 	double x = Math.PI;

	@Benchmark
	public void measure() {
		x++;
	}
}

Benchmark                           Mode  Cnt          Score   Error  Units
JMHSample_04_DefaultState.measure  thrpt       545266394.109          ops/s
```



### @Setup & @TearDown

```java
@Setup // 启动Benchmark 之前做准备工作, 必须在@State标识的类中使用，实际上是@State标识类的生命周期的一部分
public void prepare() {
	x = Math.PI;
    System.out.println("----- do Setup");
}

@TearDown // Benchmark 结束之后做收尾工作, 必须在@State标识的类中使用，实际上是@State标识类的生命周期的一部分
public void check() {
    System.out.println("----- do TearDown");
}

@Benchmark
public void measureRight() {
    x++;
}

@Benchmark
public void measureWrong() {
    double x = 0;
    x++;
}


 public static void main(String[] args) throws RunnerException {
     Options opt = new OptionsBuilder()
         .include(JMHSample_05_StateFixtures.class.getSimpleName())
         .forks(1)
         .jvmArgs("-ea")
         .build();

     new Runner(opt).run();
 }
```



```java
# Benchmark: org.openjdk.jmh.samples.JMHSample_05_StateFixtures.measureRight

# Run progress: 0.00% complete, ETA 00:00:04
# Fork: 1 of 1
# Warmup Iteration   1: ----- do Setup
531640672.812 ops/s
Iteration   1: ----- do TearDown
554361599.723 ops/s

    
# Benchmark: org.openjdk.jmh.samples.JMHSample_05_StateFixtures.measureWrong

# Run progress: 50.00% complete, ETA 00:00:02
# Fork: 1 of 1
# Warmup Iteration   1: ----- do Setup
4497489243.589 ops/s
Iteration   1: ----- do TearDown
4526285173.485 ops/s
    
Benchmark                                 Mode  Cnt           Score   Error  Units
JMHSample_05_StateFixtures.measureRight  thrpt        529834411.876          ops/s
JMHSample_05_StateFixtures.measureWrong  thrpt       3867906327.891          ops/s
```



#### Level.Trial

> ```
> @Setup(Level.Trial) // 整个Benchmark测试开始前会被执行一次，后面不再执行
> @TearDown(Level.Trial) // 整个Benchmark测试完成后才会被执行一次，后面不再执行
> ```

```java
@Setup(Level.Trial)
public void init() {
	System.out.println("----- do Setup");
}

@TearDown(Level.Trial)
public void check() {
	System.out.println("----- do TearDown");
}

# Warmup Iteration   1: ----- do Setup
4421937429.452 ops/s
# Warmup Iteration   2: 4485015612.898 ops/s
# Warmup Iteration   3: 4458406467.342 ops/s
Iteration   1: 4490684681.514 ops/s
Iteration   2: 4480366157.457 ops/s
Iteration   3: ----- do TearDown
4491445447.792 ops/s
```



#### Level.Iteration

> ```
> @Setup(Level.Iteration) // 每一轮Benchmark测试开始前会被执行一次
> @TearDown(Level.Iteration) // 每一轮Benchmark测试完成后才会被执行一次
> ```

```java
@Setup(Level.Iteration)
public void init() {
	System.out.println("----- do Setup");
}

@TearDown(Level.Iteration)
public void check() {
	System.out.println("----- do TearDown");
}

# Warmup Iteration   1: ----- do Setup
----- do TearDown
498103233.061 ops/s
# Warmup Iteration   2: ----- do Setup
----- do TearDown
519591601.900 ops/s
# Warmup Iteration   3: ----- do Setup
----- do TearDown
547577377.973 ops/s
Iteration   1: ----- do Setup
----- do TearDown
553250593.661 ops/s
Iteration   2: ----- do Setup
----- do TearDown
551605708.992 ops/s
Iteration   3: ----- do Setup
----- do TearDown
553137249.413 ops/s
```





#### Level.Invocation

> ```
> @Setup(Level.Invocation) // 每次方法被调用，都会被执行一次
> @TearDown(Level.Invocation) // 每次方法被调用完后，都会被执行一次
> ```

```java
@Setup(Level.Invocation)
public void init() {
	System.out.println("----- do Setup");
}

@TearDown(Level.Invocation)
public void check() {
	System.out.println("----- do TearDown");
}
```



## 冷启动和热启动

```java
// 模拟线程池的冷启动和热启动, 线程池启动是需要耗时的，这里面假设耗时为10ms
org.openjdk.jmh.samples.JMHSample_07_FixtureLevelInvocation


Benchmark                                        Mode  Cnt    Score   Error  Units
JMHSample_07_FixtureLevelInvocation.measureCold  avgt    2  122.002          us/op
JMHSample_07_FixtureLevelInvocation.measureHot   avgt    2    6.787          us/op
```



## DeadCode

> org.openjdk.jmh.samples.JMHSample_08_DeadCode
>
> 因为JMH使用不当，导致一些Benchmark被JVM优化掉，测试不出真实执行效率

```java
// 这个方法因为没有返回值会被JVM优化掉
// JVM通过方法内联和逃逸检测，发现没有使用方法返回值，所以compute(x); 这行代码就会被优化掉，导致和空方法的执行效率基本一致
@Benchmark
public void measureWrong() {
    compute(x);
}

public static void main(String[] args) throws RunnerException {
     Options opt = new OptionsBuilder()
     	.include(JMHSample_08_DeadCode.class.getSimpleName())
     	.forks(1)
     	.jvmArgs("-server") // 这里设置为server模式，以充分使用JIT
     	.build();

    new Runner(opt).run();
}

Benchmark                           Mode  Cnt  Score   Error  Units
JMHSample_08_DeadCode.baseline      avgt    2  0.231          ns/op
JMHSample_08_DeadCode.measureRight  avgt    2  8.931          ns/op
JMHSample_08_DeadCode.measureWrong  avgt    2  0.299          ns/op
```





```java
 public static void main(String[] args) throws RunnerException {
     Options opt = new OptionsBuilder()
     	.include(JMHSample_08_DeadCode.class.getSimpleName())
     	.forks(1)
     	.build();

    new Runner(opt).run();
}

Benchmark                           Mode  Cnt  Score   Error  Units
JMHSample_08_DeadCode.baseline      avgt    2  0.225          ns/op
JMHSample_08_DeadCode.measureRight  avgt    2  8.909          ns/op
JMHSample_08_DeadCode.measureWrong  avgt    2  0.223          ns/op
```





## blackhole

>只有在jdk8下才有意义



```java
@Benchmark
public double baseline() {
    return compute(x1);
}

@Benchmark
public double measureWrong() {
    compute(x1); // JVM通过方法内联和逃逸检测，发现没有使用方法返回值，所以compute(x1); 这行代码就会进行JIT优化被优化掉，导致和空方法的执行效率基本一致
    return compute(x2);
}

// 可能把两个参数的方法相加，这样这两个参数都会在computer方法中计算
@Benchmark
public double measureRight_1() {
    return compute(x1) + compute(x2);
}

// 可以通过黑洞操作，这样JVM就认为这两个方法都是需要执行不能优化掉
@Benchmark
public void measureRight_2(Blackhole bh) {
    bh.consume(compute(x1));
    bh.consume(compute(x2));
}

Benchmark                               Mode  Cnt   Score   Error  Units
JMHSample_09_Blackholes.baseline        avgt        9.947          ns/op
JMHSample_09_Blackholes.measureRight_1  avgt       18.611          ns/op
JMHSample_09_Blackholes.measureRight_2  avgt       18.246          ns/op
JMHSample_09_Blackholes.measureWrong    avgt        9.267          ns/op
```



## constant fold 常量折叠

> org.openjdk.jmh.samples.JMHSample_10_ConstantFold
>
> 编译时简化常数的过程
>
> 这三方法测试时间基本一致，是因为在运行时进行了常量折叠
>
> - 返回值是常量的方法
> - 对常量进行一通计算仍得到一个常量
> - 入参是final类型的成员变量

```

Benchmark                                 Mode  Cnt  Score   Error  Units
JMHSample_10_ConstantFold.baseline        avgt       1.666          ns/op
JMHSample_10_ConstantFold.measureWrong_1  avgt       1.647          ns/op
JMHSample_10_ConstantFold.measureWrong_2  avgt       1.545          ns/op
JMHSample_10_ConstantFold.measureRight    avgt       9.117          ns/op
```



## Loops

```java
@Benchmark
@OperationsPerInvocation(10) //告诉JMH 这个Benchmark运行一次相当于运行了10次；也就是说这个Benckmark虽然只被JVM运行了一次，但是JMH在计算报表时会把这一次当作10次来算
public int measureWrong_10() {
    return reps(10);
}
```



> 可以看出后面计算一次的耗时越来越快，最后执行一次只要0.017ns，JVM把多次计算进行了合并通过别的方式快速计算出来结果，这样在循环里面得到两个数相加的耗时是不正确的
>
> 我们只需要在代码里面正常写Benchmark，不需要自作聪明的加循环，JMH在执行Benckmark时后通过Annotation Processor一套规范生成执行代码,会自动进行循环，不需要自己特意地在Benchmark里面自己做循环，JMH已经帮你做好的

```java
control.announceWarmdownReady();
try {
    while (control.warmdownShouldWait) {
        blackhole.consume(l_jmhsample_11_loops0_0.measureRight());
        if (control.shouldYield) Thread.yield();
        res.allOps++;
    }
} catch (Throwable e) {
    if (!(e instanceof InterruptedException)) throw e;
}
```

```
Benchmark                               Mode  Cnt  Score   Error  Units
JMHSample_11_Loops.measureRight         avgt       1.555          ns/op
JMHSample_11_Loops.measureWrong_1       avgt       1.287          ns/op
JMHSample_11_Loops.measureWrong_10      avgt       0.156          ns/op
JMHSample_11_Loops.measureWrong_100     avgt       0.016          ns/op
JMHSample_11_Loops.measureWrong_1000    avgt       0.024          ns/op
JMHSample_11_Loops.measureWrong_10000   avgt       0.018          ns/op
JMHSample_11_Loops.measureWrong_100000  avgt       0.017          ns/op
```



## Fork

### fork(0)

> fork(0) 启动JMH的JVM进程和执行Benchmark的JVM进程是在同一个进程

```java
@Benchmark
@Fork(0)
public int measure1_c1(){
    return 1;
}

public static void printProcessID(String name) {
    System.out.println("----------------------------------------------------------------");
    System.out.println(name + " pid is " + ManagementFactory.getRuntimeMXBean().getName());
    System.out.println("----------------------------------------------------------------");
}

----------------------------------------------------------------
main pid is 20864@Chris
----------------------------------------------------------------

# Warmup Iteration   1: 
----------------------------------------------------------------
setup pid is 20864@Chris
----------------------------------------------------------------
0.518 ns/op
Iteration   1: 0.457 ns/op

Benchmark                           Mode  Cnt  Score   Error  Units
JMHSample_12_Forking_0.measure1_c1  avgt       0.457          ns/op
```



### fork(1)



>fork(1) 启动JMH的JVM进程和执行Benchmark的JVM进程是在不同进程
>
>JMH在执行Benchmar测试时会fork出一个全新的JVM进程进行测试

```java
@Benchmark
@Fork(1)
public int measure1_c1(){
    return 1;
}

----------------------------------------------------------------
main pid is 13352@Chris
----------------------------------------------------------------

# Fork: 1 of 1
# Warmup Iteration   1: 
----------------------------------------------------------------
setup pid is 11976@Chris
----------------------------------------------------------------
1.676 ns/op
Iteration   1: 1.681 ns/op


Benchmark                           Mode  Cnt  Score   Error  Units
JMHSample_12_Forking_0.measure1_c1  avgt       1.681          ns/op
```



### fork(10)

> fork(10) 表示整个JMH fork出了10个JVM进行依次去执行Benchmark测试，
>
> 不是并行去执行Benchmark测试，而是创建一个JVM进程执行完Benchmark测试后再销毁这个JVM，再创建再执行再销毁这么一个过程，总共将benchmark测试在不同的JVM进程中测试10次

```java
@State(Scope.Thread)
@BenchmarkMode(Mode.AverageTime)
@Warmup(iterations = 2,time = 1)
@Measurement(iterations = 2, time = 1)
@OutputTimeUnit(TimeUnit.NANOSECONDS)
public class JMHSample_12_Forking_1 {

    @Setup(Level.Trial)
    public void setup(){
        printProcessID("setup");
    }

    @Benchmark
    @Fork(10)
    public int measure1_c1(){
        return 1;
    }
    public static void printProcessID(String name) {
        System.out.println("----------------------------------------------------------------");
        System.out.println(name + " pid is " + ManagementFactory.getRuntimeMXBean().getName());
        System.out.println("----------------------------------------------------------------");
    }

    public static void main(String[] args) throws RunnerException {
        printProcessID("main");
        Options opt = new OptionsBuilder()
                .include(JMHSample_12_Forking_1.class.getSimpleName())
                .build();

        new Runner(opt).run();
    }

}



org.openjdk.jmh.samples.JMHSample_12_Forking_1
----------------------------------------------------------------
main pid is 8368@Chris
----------------------------------------------------------------
# JMH version: 1.38-SNAPSHOT
# VM version: JDK 1.8.0_361, Java HotSpot(TM) 64-Bit Server VM, 25.361-b09
# VM invoker: C:\Program Files\Java\jdk1.8.0_361\jre\bin\java.exe
# VM options: -javaagent:C:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\lib\idea_rt.jar=52902:C:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\bin -Dfile.encoding=UTF-8
# Blackhole mode: full + dont-inline hint (auto-detected, use -Djmh.blackhole.autoDetect=false to disable)
# Warmup: 2 iterations, 1 s each
# Measurement: 2 iterations, 1 s each
# Timeout: 10 min per iteration
# Threads: 1 thread, will synchronize iterations
# Benchmark mode: Average time, time/op
# Benchmark: org.openjdk.jmh.samples.JMHSample_12_Forking_1.measure1_c1

# Run progress: 0.00% complete, ETA 00:00:40
# Fork: 1 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 14660@Chris
----------------------------------------------------------------
1.578 ns/op
# Warmup Iteration   2: 1.673 ns/op
Iteration   1: 1.241 ns/op
Iteration   2: 1.110 ns/op

# Run progress: 10.00% complete, ETA 00:00:43
# Fork: 2 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 11336@Chris
----------------------------------------------------------------
1.421 ns/op
# Warmup Iteration   2: 1.440 ns/op
Iteration   1: 1.147 ns/op
Iteration   2: 1.068 ns/op

# Run progress: 20.00% complete, ETA 00:00:38
# Fork: 3 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 4904@Chris
----------------------------------------------------------------
1.400 ns/op
# Warmup Iteration   2: 1.434 ns/op
Iteration   1: 1.062 ns/op
Iteration   2: 1.079 ns/op

# Run progress: 30.00% complete, ETA 00:00:33
# Fork: 4 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 18992@Chris
----------------------------------------------------------------
1.383 ns/op
# Warmup Iteration   2: 1.444 ns/op
Iteration   1: 1.074 ns/op
Iteration   2: 1.073 ns/op

# Run progress: 40.00% complete, ETA 00:00:28
# Fork: 5 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 15644@Chris
----------------------------------------------------------------
1.396 ns/op
# Warmup Iteration   2: 1.481 ns/op
Iteration   1: 1.067 ns/op
Iteration   2: 1.067 ns/op

# Run progress: 50.00% complete, ETA 00:00:23
# Fork: 6 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 20944@Chris
----------------------------------------------------------------
1.421 ns/op
# Warmup Iteration   2: 1.435 ns/op
Iteration   1: 1.070 ns/op
Iteration   2: 1.071 ns/op

# Run progress: 60.00% complete, ETA 00:00:19
# Fork: 7 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 20208@Chris
----------------------------------------------------------------
1.370 ns/op
# Warmup Iteration   2: 1.440 ns/op
Iteration   1: 1.068 ns/op
Iteration   2: 1.062 ns/op

# Run progress: 70.00% complete, ETA 00:00:14
# Fork: 8 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 1656@Chris
----------------------------------------------------------------
1.386 ns/op
# Warmup Iteration   2: 1.437 ns/op
Iteration   1: 1.082 ns/op
Iteration   2: 1.066 ns/op

# Run progress: 80.00% complete, ETA 00:00:09
# Fork: 9 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 12804@Chris
----------------------------------------------------------------
1.395 ns/op
# Warmup Iteration   2: 1.444 ns/op
Iteration   1: 1.067 ns/op
Iteration   2: 1.087 ns/op

# Run progress: 90.00% complete, ETA 00:00:04
# Fork: 10 of 10
# Warmup Iteration   1: ----------------------------------------------------------------
setup pid is 14188@Chris
----------------------------------------------------------------
1.396 ns/op
# Warmup Iteration   2: 1.455 ns/op
Iteration   1: 1.067 ns/op
Iteration   2: 1.067 ns/op


Result "org.openjdk.jmh.samples.JMHSample_12_Forking_1.measure1_c1":
  1.085 ±(99.9%) 0.036 ns/op [Average]
  (min, avg, max) = (1.062, 1.085, 1.241), stdev = 0.042
  CI (99.9%): [1.049, 1.121] (assumes normal distribution)


# Run complete. Total time: 00:00:47	

Benchmark                           Mode  Cnt  Score   Error  Units
JMHSample_12_Forking_1.measure1_c1  avgt   20  1.085 ± 0.036  ns/op
```



### fork()

> fork()  fork里面为空，默认表示fork出5个进程,但不建议使用默认值，这样会降低代码的可读性，别人看你代码或者过两天你看自己的代码不知道是想干啥





### 同一进程中的干扰问题

```java
Benchmark                                 Mode  Cnt  Score   Error  Units
JMHSample_12_Forking.measure_1_c1         avgt       1.213          ns/op
JMHSample_12_Forking.measure_2_c2         avgt       4.182          ns/op
JMHSample_12_Forking.measure_3_c1_again   avgt       4.851          ns/op
JMHSample_12_Forking.measure_4_forked_c1  avgt       1.997          ns/op
JMHSample_12_Forking.measure_5_forked_c2  avgt       1.987          ns/op
```



```java
public static class Counter1 implements Counter {
    private int x;

    @Override
    public int inc() {
        return x++;
    }
}

public int measure(Counter c) {
    int s = 0;
    for (int i = 0; i < 10; i++) {
        s += c.inc();
    }
    return s;
}
```



> 在调用每个c1的benckmark时传入的是c1，这时 `c.inc()` 就是 `c1.inc()`, JVM解释执行它需要先找到c1的对象，再执行c1的 `inc()`方法，这个在我们的代码里面是体现不出来的，但是JVM的确又是这么做的。
>
> 第一个传入的参数是c1，JVM就会假设这个类型参数都是c1，再进行一些激进的优化，比如方法内联，在运行时JIT把c.inc()变为x++， 这样 `int inc()` 这个方法就没有了，第一次执行时这个方法的效率会非常高。
>
> 当执行到第二个benchmark时，因为此时都是在同一个JVM里面，JVM记录的Counter实例都是c1，这时我们传入了一个c2,导致我们的 JIT 优化失效，JVM优化降级又转为了解释执行，放弃了方法内联的方式，在执行c2时，会先找到c2这个对象，再去c2对象里面到 `int inc()` 方法后再执行
>
> 因此，在同个JVM里面多个benchmark是可以相互影响的， 有的时候JVM会优化，有时又因为你的benchmark写的有问题又不优化，所以在进行benchmark测试时尽量放到不同的JVM进程中



> 《Java虚拟机规范》 字节码指令invokeinterface
>
> 《深入了解Java虚拟机》第8章 8.4.2
>
> 《深入理解Java虚拟机》第11章 11.4.2



### 什么时候用fork

> 可以看到在JMH启动时这个随机值是已经确认在，在整个Benchmark测试过程中使用的都是一个确定的值
>
> 但每次执行得到的随机数都是不一样的，的这就带来一个问题，如何得到一个偏差较小，更接近我们期望值的数据，这时就要使用到fork

```java
@State(Scope.Thread)
public static class SleepyState {
    public long sleepTime;

    @Setup
    public void setup() {
        sleepTime = (long) (Math.random() * 1000);
        System.out.println("----------------------");
        System.out.println("sleepTime:" + sleepTime);
        System.out.println("----------------------");
    }
}

Benchmark                       Mode  Cnt    Score     Error  Units
JMHSample_13_RunToRun.baseline  avgt    3  118.507 ±   0.884  ms/op
JMHSample_13_RunToRun.fork_1    avgt   15  696.184 ± 187.366  ms/op
```



> 如果使用到的算法有一定的随机性，比如会生成一个随机值，然后在后面的执行中都会使用到这个随机值，这个随机值是如何分布的，一次或多次的测试是体现不出来的，
>
> 比如我们会有一些随机算法，在启动的时候生成一个种子，在整个执行过程的生成的随机数都会基于这个种子，为了使结果尽可能的平均，接近我们的期望值，减少偏差，就要多测试几轮
>
> 每轮测试都放到一个新的JVM进程中独立的执行



