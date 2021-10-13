SINGULARITY_USER = lee0767

.PHONY: docker pushsif

docker:
	cd docker && docker build -t kofamscan-ubuntu16:1.3.0 .

sif:
	singularity build kofamscan-ubuntu16_1.3.0.sif docker-daemon://kofamscan-ubuntu16:1.3.0

pushsif:
	singularity sign kofamscan-ubuntu16_1.3.0.sif
	singularity push kofamscan-ubuntu16_1.3.0.sif library://$(SINGULARITY_USER)/default/kofamscan-ubuntu16:1.3.0

clean:
	rm kofamscan-ubuntu16_1.3.0.sif
