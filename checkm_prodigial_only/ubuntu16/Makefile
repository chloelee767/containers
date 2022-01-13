SINGULARITY_USER = lee0767

.PHONY: docker pushsif

docker:
	cd docker && docker build --build-arg VER=1.1.3 --no-cache -t checkm-prodigial-only-ubuntu16:1.1.3 .

sif:
	singularity build checkm-prodigial-only-ubuntu16_1.1.3.sif docker-daemon://checkm-prodigial-only-ubuntu16:1.1.3

pushsif:
	singularity sign checkm-prodigial-only-ubuntu16_1.1.3.sif
	singularity push checkm-prodigial-only-ubuntu16_1.1.3.sif library://$(SINGULARITY_USER)/default/checkm-prodigial-only-ubuntu16:1.1.3

clean:
	rm checkm-ubuntu16_1.1.3.sif
