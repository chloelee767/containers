SINGULARITY_USER = lee0767

.PHONY: docker pushsif

docker:
	cd docker && docker build --build-arg VER=1.1.3 --no-cache -t checkm-ubuntu16:1.1.3 .

sif:
	singularity build checkm-ubuntu16_1.1.3.sif docker-daemon://checkm-ubuntu16:1.1.3

pushsif:
	singularity sign checkm-ubuntu16_1.1.3.sif
	singularity push checkm-ubuntu16_1.1.3.sif library://$(SINGULARITY_USER)/default/checkm-ubuntu16:1.1.3

clean:
	rm checkm-ubuntu16_1.1.3.sif
