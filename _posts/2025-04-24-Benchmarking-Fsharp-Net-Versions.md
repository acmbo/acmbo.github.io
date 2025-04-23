## Benchmarking Net Versions of F#

Many CAD programs have API's, which expose to .Net code. I recent years, the bigger players shifted away from NetFramework48 to more current Net Versions like 7 or 8. Best examples are the recent versions of Revit and Rhino. 

I wanted to see some of the influence of the Net version asside from cross platfrom compilation and langugage features like perfromance.

### A simple and naive approach to perfromance benchmarks

Since i'm not really familier with benchmark, especially between differen .Net versions, i wanted to start with something small and easy. I picked a naive fibonacci computation, which is easy to implement in all versions of Net:

```
open System
open BenchmarkDotNet.Attributes
open BenchmarkDotNet.Running

type FibonacciBenchmark() =

    [<Params(10, 20, 30)>]
    member val N = 0 with get, set

    [<Benchmark>]
    member this.NaiveFibonacci() =
        let rec fib n =
            if n <= 1 then n
            else fib (n - 1) + fib (n - 2)
        fib this.N

[<EntryPoint>]
let main argv =
    BenchmarkRunner.Run<FibonacciBenchmark>() |> ignore
    0
```

#### Results in Net8
```
BenchmarkDotNet v0.14.0, Windows 10 (22H2/2022Update)
Intel Core i7-10850H CPU 2.70GHz, 1 CPU, 12 logical and 6 physical cores
.NET SDK 8.0.100
  [Host]     : .NET 8.0.0 (8.0.23.53103), X64 RyuJIT AVX2 DEBUG
  DefaultJob : .NET 8.0.0 (8.0.23.53103), X64 RyuJIT AVX2

// * Hints *
Outliers
FibonacciBenchmark.NaiveFibonacci: Default -> 3 outliers were removed (178.55 ns..184.25 ns)

// * Legends *
N      : Value of the 'N' parameter
Mean   : Arithmetic mean of all measurements
Error  : Half of 99.9% confidence interval
StdDev : Standard deviation of all measurements
1 ns   : 1 Nanosecond (0.000000001 sec)
```

| Method         | N  | Mean           | Error        | StdDev       |
|--------------- |--- |---------------:|-------------:|-------------:|
| NaiveFibonacci | 10 |       166.6 ns |      2.95 ns |      2.62 ns |
| NaiveFibonacci | 20 |    20,289.3 ns |    196.96 ns |    184.24 ns |
| NaiveFibonacci | 30 | 2,497,391.2 ns | 33,438.25 ns | 31,278.16 ns |


#### Results in Net7

```
BenchmarkDotNet v0.14.0, Windows 10 (22H2/2022Update)
Intel Core i7-10850H CPU 2.70GHz, 1 CPU, 12 logical and 6 physical cores
.NET SDK 8.0.100
  [Host]     : .NET 7.0.14 (7.0.1423.51910), X64 RyuJIT AVX2 DEBUG
  DefaultJob : .NET 7.0.14 (7.0.1423.51910), X64 RyuJIT AVX2

// * Hints *
Outliers
  FibonacciBenchmark.NaiveFibonacci: Default -> 1 outlier  was  removed, 3 outliers were detected (28.88 us, 28.91 us, 30.03 us)
  FibonacciBenchmark.NaiveFibonacci: Default -> 1 outlier  was  removed (4.04 ms)

// * Legends *
  N      : Value of the 'N' parameter
  Mean   : Arithmetic mean of all measurements
  Error  : Half of 99.9% confidence interval
  StdDev : Standard deviation of all measurements
  1 ns   : 1 Nanosecond (0.000000001 sec)
```

| Method         | N  | Mean           | Error        | StdDev        |
|--------------- |--- |---------------:|-------------:|--------------:|
| NaiveFibonacci | 10 |       234.9 ns |      4.10 ns |       3.84 ns |
| NaiveFibonacci | 20 |    29,275.7 ns |    215.79 ns |     191.29 ns |
| NaiveFibonacci | 30 | 3,610,084.6 ns | 71,173.70 ns | 112,889.05 ns |



#### Results in Net6
```
BenchmarkDotNet v0.14.0, Windows 10 (22H2/2022Update)
Intel Core i7-10850H CPU 2.70GHz, 1 CPU, 12 logical and 6 physical cores
.NET SDK 8.0.100
  [Host]     : .NET 6.0.25 (6.0.2523.51912), X64 RyuJIT AVX2 DEBUG
  DefaultJob : .NET 6.0.25 (6.0.2523.51912), X64 RyuJIT AVX2

// * Hints *
Outliers
  FibonacciBenchmark.NaiveFibonacci: Default -> 2 outliers were removed (32.85 us, 33.08 us)
  FibonacciBenchmark.NaiveFibonacci: Default -> 2 outliers were removed (3.96 ms, 3.99 ms)

// * Legends *
  N      : Value of the 'N' parameter
  Mean   : Arithmetic mean of all measurements
  Error  : Half of 99.9% confidence interval
  StdDev : Standard deviation of all measurements
  1 ns   : 1 Nanosecond (0.000000001 sec)
```

| Method         | N  | Mean           | Error        | StdDev       |
|--------------- |--- |---------------:|-------------:|-------------:|
| NaiveFibonacci | 10 |       262.9 ns |      4.51 ns |      4.22 ns |
| NaiveFibonacci | 20 |    32,163.7 ns |    253.10 ns |    211.35 ns |
| NaiveFibonacci | 30 | 3,846,234.8 ns | 23,758.98 ns | 19,839.83 ns |



#### Results in NetFramework48

```
BenchmarkDotNet v0.14.0, Windows 10 (22H2/2022Update)
Intel Core i7-10850H CPU 2.70GHz, 1 CPU, 12 logical and 6 physical cores
  [Host]     : .NET Framework 4.8 (4.8.4772.0), X64 LegacyJIT VectorSize=256 DEBUG
  DefaultJob : .NET Framework 4.8 (4.8.4772.0), X64 RyuJIT VectorSize=256

// * Hints *
Outliers
  FibonacciBenchmark.NaiveFibonacci: Default -> 7 outliers were removed (36.27 us..140.75 us)
  FibonacciBenchmark.NaiveFibonacci: Default -> 2 outliers were removed (4.23 ms, 4.29 ms)

// * Legends *
  N      : Value of the 'N' parameter
  Mean   : Arithmetic mean of all measurements
  Error  : Half of 99.9% confidence interval
  StdDev : Standard deviation of all measurements
  1 ns   : 1 Nanosecond (0.000000001 sec)
```
| Method         | N  | Mean           | Error        | StdDev        |
|--------------- |--- |---------------:|-------------:|--------------:|
| NaiveFibonacci | 10 |       260.0 ns |      5.00 ns |       4.68 ns |
| NaiveFibonacci | 20 |    32,212.2 ns |    573.15 ns |     957.60 ns |
| NaiveFibonacci | 30 | 3,959,601.8 ns | 74,595.78 ns | 104,572.87 ns |
