Issue 48088 reproducer
===

See https://github.com/golang/go/issues/48088

```
$ go version
go version go1.17 linux/amd64
$ go build .
# issue-48088-repro
panic: runtime error: invalid memory address or nil pointer dereference
[signal SIGSEGV: segmentation violation code=0x1 addr=0x38 pc=0x5baad9]

goroutine 1 [running]:
cmd/compile/internal/ir.MethodExprName(...)
	/usr/local/go/src/cmd/compile/internal/ir/expr.go:1067
cmd/compile/internal/ir.(*bottomUpVisitor).visit.func2({0xe4ed88, 0xc0003760c0})
	/usr/local/go/src/cmd/compile/internal/ir/scc.go:94 +0xd9
cmd/compile/internal/ir.Visit.func1({0xe4ed88, 0xc0003760c0})
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:105 +0x30
cmd/compile/internal/ir.doNodes({0xc00009e9f0, 0x1, 0x7f5a8676ffff}, 0xc0000ac708)
	/usr/local/go/src/cmd/compile/internal/ir/node_gen.go:1440 +0x67
cmd/compile/internal/ir.(*AssignListStmt).doChildren(0xc0003761e0, 0xc0003761e0)
	/usr/local/go/src/cmd/compile/internal/ir/node_gen.go:100 +0x7f
cmd/compile/internal/ir.DoChildren(...)
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:94
cmd/compile/internal/ir.Visit.func1({0xe4cd80, 0xc0003761e0})
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:106 +0x57
cmd/compile/internal/ir.doNodes({0xc0000b9a80, 0x3, 0x7f5a8658bd00}, 0xc0000ac708)
	/usr/local/go/src/cmd/compile/internal/ir/node_gen.go:1440 +0x67
cmd/compile/internal/ir.(*BlockStmt).doChildren(0xc0000b9a40, 0xc0000b9a40)
	/usr/local/go/src/cmd/compile/internal/ir/node_gen.go:222 +0x57
cmd/compile/internal/ir.DoChildren(...)
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:94
cmd/compile/internal/ir.Visit.func1({0xe4d168, 0xc0000b9a40})
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:106 +0x57
cmd/compile/internal/ir.doNodes({0xc0000a1fb0, 0x3, 0xc0003780e0}, 0xc0000ac708)
	/usr/local/go/src/cmd/compile/internal/ir/node_gen.go:1440 +0x67
cmd/compile/internal/ir.(*BlockStmt).doChildren(0xc0000b9ac0, 0xc0000b9ac0)
	/usr/local/go/src/cmd/compile/internal/ir/node_gen.go:222 +0x57
cmd/compile/internal/ir.DoChildren(...)
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:94
cmd/compile/internal/ir.Visit.func1({0xe4d168, 0xc0000b9ac0})
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:106 +0x57
cmd/compile/internal/ir.doNodes({0xc00009e8c0, 0x1, 0x0}, 0xc0000ac708)
	/usr/local/go/src/cmd/compile/internal/ir/node_gen.go:1440 +0x67
cmd/compile/internal/ir.(*Func).doChildren(0xe4dac8, 0xc0000fa2c0)
	/usr/local/go/src/cmd/compile/internal/ir/func.go:151 +0x2e
cmd/compile/internal/ir.DoChildren(...)
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:94
cmd/compile/internal/ir.Visit.func1({0xe4dac8, 0xc0000fa2c0})
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:106 +0x57
cmd/compile/internal/ir.Visit({0xe4dac8, 0xc0000fa2c0}, 0xc00009ea50)
	/usr/local/go/src/cmd/compile/internal/ir/visit.go:108 +0xb8
cmd/compile/internal/ir.(*bottomUpVisitor).visit(0xc00037a000, 0xc0000fa2c0)
	/usr/local/go/src/cmd/compile/internal/ir/scc.go:87 +0x1b3
cmd/compile/internal/ir.VisitFuncsBottomUp({0xc00009e8e0, 0x1, 0x2}, 0xd16550)
	/usr/local/go/src/cmd/compile/internal/ir/scc.go:60 +0x105
cmd/compile/internal/escape.Funcs(...)
	/usr/local/go/src/cmd/compile/internal/escape/escape.go:1821
cmd/compile/internal/gc.Main(0xd16450)
	/usr/local/go/src/cmd/compile/internal/gc/main.go:253 +0xcef
main.main()
	/usr/local/go/src/cmd/compile/main.go:55 +0xdd
```