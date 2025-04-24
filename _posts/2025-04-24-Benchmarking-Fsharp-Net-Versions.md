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

Generell Setup remarks: 

```
BenchmarkDotNet v0.14.0, Windows 10 (22H2/2022Update)
Intel Core i7-10850H CPU 2.70GHz, 1 CPU, 12 logical and 6 physical cores

// * Legends *
N      : Value of the 'N' parameter
Mean   : Arithmetic mean of all measurements
Error  : Half of 99.9% confidence interval
StdDev : Standard deviation of all measurements
1 ns   : 1 Nanosecond (0.000000001 sec)
```

All tests regarding the NetVersions are done with FSharp.Core (8.0.100)

#### Results of different Net versions

```
.NET SDK 8.0.100
  [Host]     : .NET 8.0.0 (8.0.23.53103), X64 RyuJIT AVX2 DEBUG
  DefaultJob : .NET 8.0.0 (8.0.23.53103), X64 RyuJIT AVX2

  [Host]     : .NET 7.0.14 (7.0.1423.51910), X64 RyuJIT AVX2 DEBUG
  DefaultJob : .NET 7.0.14 (7.0.1423.51910), X64 RyuJIT AVX2

  [Host]     : .NET 6.0.25 (6.0.2523.51912), X64 RyuJIT AVX2 DEBUG
  DefaultJob : .NET 6.0.25 (6.0.2523.51912), X64 RyuJIT AVX2

  [Host]     : .NET Framework 4.8 (4.8.4772.0), X64 LegacyJIT VectorSize=256 DEBUG
  DefaultJob : .NET Framework 4.8 (4.8.4772.0), X64 RyuJIT VectorSize=256
```

| Method                            | N  | Mean           | Error        | StdDev       |
|---------------------------------- |--- |---------------:|-------------:|-------------:|
| NaiveFibonacci .NET 8.0.0         | 30 | 2,497,391.2 ns | 33,438.25 ns | 31,278.16 ns |
| NaiveFibonacci .NET 7.0.14        | 30 | 3,610,084.6 ns | 71,173.70 ns | 112,889.05 ns|
| NaiveFibonacci .NET 6.0.25        | 30 | 3,846,234.8 ns | 23,758.98 ns | 19,839.83 ns |
| NaiveFibonacci .NET Framework 4.8 | 30 | 3,959,601.8 ns | 74,595.78 ns | 104,572.87 ns|

### Comparison between FSharpCore Versions

```
BenchmarkDotNet v0.14.0, Windows 10 (10.0.19045.5608/22H2/2022Update)
Intel Core i7-10850H CPU 2.70GHz, 1 CPU, 12 logical and 6 physical cores
.NET SDK 8.0.100
  [Host]     : .NET 8.0.0 (8.0.23.53103), X64 RyuJIT AVX2 DEBUG
  DefaultJob : .NET 8.0.0 (8.0.23.53103), X64 RyuJIT AVX2

// * Legends *
  N      : Value of the 'N' parameter
  Mean   : Arithmetic mean of all measurements
  Error  : Half of 99.9% confidence interval
  StdDev : Standard deviation of all measurements
  1 ms   : 1 Millisecond (0.001 sec)
```
| Method                               | N  | Mean     | Error     | StdDev    |
|------------------------------------- |--- |---------:|----------:|----------:|
| NaiveFibonacci Fsharp.Core (6.0.0)   | 30 | 3.080 ms | 0.0599 ms | 0.0500 ms |
| NaiveFibonacci Fsharp.Core (7.0.0)   | 30 | 3.393 ms | 0.0804 ms | 0.2319 ms |
| NaiveFibonacci Fsharp.Core (8.0.100) | 30 | 3.205 ms | 0.0640 ms | 0.1278 ms |
| NaiveFibonacci Fsharp.Core (9.0.202) | 30 | 3.113 ms | 0.0587 ms | 0.0521 ms |


| Method                               | Mean     | Error   | StdDev  |
|------------------------------------- |---------:|--------:|--------:|
| MandelbrotTest Fsharp.Core (6.0.0)   | 345.2 us | 4.45 us | 3.94 us |
| MandelbrotTest Fsharp.Core (7.0.0)   | 282.0 us | 2.28 us | 2.13 us |
| MandelbrotTest Fsharp.Core (8.0.100) | 278.2 us | 4.43 us | 4.14 us |
| MandelbrotTest Fsharp.Core (9.0.202) | 273.0 us | 3.66 us | 3.06 us |
