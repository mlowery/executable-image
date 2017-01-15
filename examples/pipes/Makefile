.PHONY: build
build:
	docker build -t exec-img-pipes-example .

.PHONY: run
run:
	echo "hello" | ./pipes-example | grep hello
