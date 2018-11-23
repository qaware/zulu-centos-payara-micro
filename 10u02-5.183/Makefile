ZULU_VERSION=10u02
PAYARA_VERSION=5
PAYARA_RELEASE=183
PAYARA_TAG=${PAYARA_VERSION}.${PAYARA_RELEASE}

docker:
	docker build --build-arg ZULU_VERSION=${ZULU_VERSION} --build-arg PAYARA_TAG=${PAYARA_TAG} --build-arg PAYARA_RELEASE=${PAYARA_RELEASE} -t zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} .

tag: docker
	docker tag zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}
	docker push qaware/zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}

latest: tag
	docker tag zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/zulu-centos-payara-micro:latest
	docker push qaware/zulu-centos-payara-micro:latest
