APPLICATION ?= helloworld

.PHONY: build
build: gomodgen
	echo $(APPLICATION)
	export GO111MODULE=on
	env GOOS=linux go build -ldflags="-s -w" -o bin/$(APPLICATION) $(APPLICATION)/main.go

.PHONY: deploy
deploy: clean build
	sls deploy --verbose

.PHONY: invoke
invoke:
	sls invoke -f $(APPLICATION)

.PHONY: invoke-local
invoke-local: build
	sls invoke local -f $(APPLICATION)

.PHONY: clean
clean:
	rm -rf ./bin ./vendor Gopkg.lock

.PHONY: remove
remove:
	sls remove

.PHONY: gomodgen
gomodgen:
	chmod u+x gomod.sh
	./gomod.sh
