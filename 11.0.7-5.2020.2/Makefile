ZULU_VERSION=11.0.7
PAYARA_VERSION=5
PAYARA_RELEASE=2020.2
PAYARA_TAG=${PAYARA_VERSION}.${PAYARA_RELEASE}

image:
	docker build --build-arg ZULU_VERSION=${ZULU_VERSION} --build-arg PAYARA_TAG=${PAYARA_TAG} --build-arg PAYARA_RELEASE=${PAYARA_RELEASE} -t zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} .
	@echo ""
	@echo "To test the image run:"
	@echo "docker run -it --rm --cpus 2 --memory 640m zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}"

tag-and-push: image
	docker tag zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}
	docker push qaware/zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}

latest: tag-and-push
	docker tag zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/zulu-centos-payara-micro:latest
	docker push qaware/zulu-centos-payara-micro:latest
