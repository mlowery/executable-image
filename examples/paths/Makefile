.PHONY: build
build:
	docker build -t exec-img-paths-example .

.PHONY: run
run:
	./paths-example hello.txt
	cp hello.txt /tmp/hello.txt
	./paths-example /tmp/hello.txt
	cp hello.txt ~
	./paths-example ~/hello.txt
