FILES:=$(wildcard out/*.go)

.PHONY: check
check: errcheck golint $(FILES:.go=.checked)

out/%.checked: out/%.go
	errcheck $<
	go vet --all $<
	golint $<

$(GOPATH)/bin/go-bindata: $(wildcard ../*.go) $(wildcard ../**/*.go)
	go install -race ../...
	$(GOPATH)/bin/go-bindata --version

out/compress-memcopy.go: $(wildcard in/**/*) $(GOPATH)/bin/go-bindata
	GO_BINDATA_TEST=true $(GOPATH)/bin/go-bindata --modtime=1136214245 -o $@ in/...

out/compress-nomemcopy.go: $(wildcard in/**/*) $(GOPATH)/bin/go-bindata
	GO_BINDATA_TEST=true $(GOPATH)/bin/go-bindata --modtime=1136214245 --nomemcopy -o $@ in/...

out/debug.go: $(wildcard in/**/*) $(GOPATH)/bin/go-bindata
	GO_BINDATA_TEST=true $(GOPATH)/bin/go-bindata --modtime=1136214245 --debug -o $@ in/...

out/nocompress-memcopy.go: $(wildcard in/**/*) $(GOPATH)/bin/go-bindata
	GO_BINDATA_TEST=true $(GOPATH)/bin/go-bindata --modtime=1136214245 --nocompress -o $@ in/...

out/nocompress-nomemcopy.go: $(wildcard in/**/*) $(GOPATH)/bin/go-bindata
	GO_BINDATA_TEST=true $(GOPATH)/bin/go-bindata --modtime=1136214245 --nocompress -nomemcopy -o $@ in/...

out/prefix.go: $(wildcard in/**/*) $(GOPATH)/bin/go-bindata
	GO_BINDATA_TEST=true $(GOPATH)/bin/go-bindata --modtime=1136214245 --prefix in -o $@ in/...

errcheck:
	go get github.com/kisielk/errcheck

golint:
	go get golang.org/x/lint/golint
