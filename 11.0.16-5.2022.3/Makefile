ZULU_VERSION=11.0.16.1
PAYARA_VERSION=5
PAYARA_RELEASE=2022.3
PAYARA_TAG=${PAYARA_VERSION}.${PAYARA_RELEASE}

# Builds a single plattform image and stores it in the local docker registry
# This command is used for testing the image locally
local-image:
	docker build --build-arg ZULU_VERSION=${ZULU_VERSION} --build-arg PAYARA_TAG=${PAYARA_TAG} --build-arg PAYARA_RELEASE=${PAYARA_RELEASE} -t zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} .
	@echo ""
	@echo "To test the image run:"
	@echo "docker run -it --rm --cpus 2 --memory 640m zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}"

# Builds a image for the architectures arm64 and amd64 and pushes it to docker hub
build-multi-arch-and-push:
	docker buildx build --platform linux/arm64/v8,linux/amd64 --push \
		--build-arg ZULU_VERSION=${ZULU_VERSION} \
		--build-arg PAYARA_TAG=${PAYARA_TAG} \
		--build-arg PAYARA_RELEASE=${PAYARA_RELEASE} \
		-t qaware/zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} .

# Pushes the cached multi arch layers under the tag "latest"
latest: build-multi-arch-and-push
	docker buildx build --platform linux/arm64/v8,linux/amd64 --push \
		--build-arg ZULU_VERSION=${ZULU_VERSION} \
		--build-arg PAYARA_TAG=${PAYARA_TAG} \
		--build-arg PAYARA_RELEASE=${PAYARA_RELEASE} \
		-t qaware/zulu-centos-payara-micro:latest .

