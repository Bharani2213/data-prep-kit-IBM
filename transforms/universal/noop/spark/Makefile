# Define the root of the local git clone for the common rules to be able 
# know where they are running from.
REPOROOT=../../../..
# Include a library of common .transform.* targets which most
# transforms should be able to reuse.  However, feel free
# to override/redefine the rules below. 

include $(REPOROOT)/transforms/.make.transforms

TRANSFORM_NAME=noop

venv::	.transforms.spark-venv

test::	.transforms.spark-test

clean:: .transforms.clean

image:: .transforms.spark-image

test-src:: .transforms.test-src

setup:: .transforms.setup

build:: build-dist image

publish: publish-image

publish-image:: .transforms.publish-image-spark

# set the version of python transform that this depends on.
set-versions: 
	$(MAKE) TRANSFORM_PYTHON_VERSION=${NOOP_PYTHON_VERSION} TOML_VERSION=$(NOOP_SPARK_VERSION) .transforms.set-versions 
        
build-dist:: .defaults.build-dist 

publish-dist:: .defaults.publish-dist

test-image:: .transforms.spark-test-image

run-cli-sample: .transforms.run-cli-spark-sample

run-local-sample: .transforms.run-local-sample

minio-start:	.minio-start

kind-load-image:: .transforms.kind-load-image

docker-load-image: .defaults.docker-load-image

docker-save-image: .defaults.docker-save-image
