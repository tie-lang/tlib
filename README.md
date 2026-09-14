# tlib — tie builtin libraries / tie 内置库

`tlib` 是 tie 语言的内置库独立仓库（t+ 词缀规范），包含四组源码库。它被 tiec 编译器用于自举编译，也被用户程序通过 `/std`、`/ext`、`/rdu`、`/sys` 别名直接引用。tiec 对内置库的零副本（zero-copy）包依赖设计正在推进中，届时 tiec 将不再维护这些目录的副本。

`tlib` is the standalone repository for the tie compiler's built-in standard libraries (per the `t+` affix-naming convention). It contains four source-library groups. It is used by the tiec compiler for self-bootstrapping and is referenced by user programs through the `/std`, `/ext`, `/rdu`, `/sys` aliases. A zero-copy package-dependency design for these libraries in tiec is under way; until then tiec maintains its own copy of the content.

## 四目录说明 / Directory overview

- `std/` — 标准库：跨平台的核心与通用能力（字符串、集合、字节、正则、编码、时间、文件、网络、HTTP、密码/哈希、JSON/YAML、数值、图像等）。
  Standard library: cross-platform core and general-purpose capabilities (strings, collections, bytes, regex, encodings, time, filesystem, network, HTTP, crypto/hash, JSON/YAML, numeric, image, etc.).
- `ext/` — 扩展库：分目录组织的可选能力（AES/ChaCha20/argon2 等密码算法、机器学习、TUI、压缩、日志、基准等）。
  Extension library: optional capabilities organized into subdirectories (AES/ChaCha20/argon2 crypto, ML, TUI, compression, logging, benchmarking, etc.).
- `rdu/` — 嵌入式开发库：面向低资源/嵌入场景的精简实现（定宽整数、CRC、RDB、精简随机与一致性探针等）。
  Embedded development library: lightweight implementations for low-resource/embedded scenarios (fixed-width ints, CRC, RDB, compact RNG and consistency probes, etc.).
- `sys/` — 平台专用层：重命名并引入 `sys_*` 平台符号集。当前含 Windows 平台实现 `sys/win32.tie`。
  Platform-specific layer: re-exported as the `sys_*` platform symbol set. Currently contains the Windows implementation `sys/win32.tie`.

## 引用与使用 / Usage

程序内通过别名引用内置库（与 tiec 自举编译的加载路径一致）：

Libraries are referenced by alias inside programs, matching the load paths used by tiec self-bootstrapping:

```tie
import /std
import /ext
import /rdu
import /sys
```

## 构建与试用 / Build & try

本仓库不含编译器。构建与运行请使用 tiec 编译器（例如在 tiec 工作区执行 tiec 自举/解释运行），内置库路径即本仓库的四目录或其别名挂载点。

This repository does not contain the compiler. To build or run tie programs, use the tiec compiler (e.g. run bootstrap/interpreter in the tiec workspace); the builtin-library paths are this repository's four directories, mounted under their aliases.

```sh
tiec run examples/hello.tie
```

## 许可证 / License

tie 内置库以 **TIE Public License 2.0（TPL 2.0）** 授权，详见 [LICENSE](LICENSE)。

The tie builtin libraries are licensed under the **TIE Public License 2.0 (TPL 2.0)**. See [LICENSE](LICENSE) for details.