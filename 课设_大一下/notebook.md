### cpp&flutter交互方案

ask AI：“我希望用flutter做前端，cpp写后端，中间怎么链接交互”

#### 通过本地进程通信

适用于 Flutter 和 C++ 在同一设备上运行（如 Flutter 桌面应用，桌面/嵌入式场景）。

##### 方法 1：通过标准输入输出（stdin/stdout）

-   **C++ 后端**：作为子进程运行，通过 stdin/stdout 与 Flutter 交互。

-   **Flutter 前端**：使用 [`dart:io`](https://api.dart.dev/stable/dart-io/dart-io-library.html) 的 `Process` 类启动 C++ 进程。

    ```dart
    import 'dart:io';
    
    Future<void> runCppProcess() async {
        final process = await Process.start('./your_cpp_executable', []);
        process.stdin.writeln('send data to C++');
        final output = await process.stdout.transform(utf8.decoder).first;
        print('C++ replied: $output');
    }
    ```