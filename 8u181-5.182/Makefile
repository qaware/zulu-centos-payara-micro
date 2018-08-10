ZULU_VERSION=8u181
PAYARA_VERSION=5
PAYARA_RELEASE=182
PAYARA_TAG=${PAYARA_VERSION}.${PAYARA_RELEASE}

docker:
	docker build -t zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} .

push: docker
	docker tag zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}
	docker push qaware/zulu-centos-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}
