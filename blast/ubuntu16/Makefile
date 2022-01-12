SINGULARITY_USER = lee0767

.PHONY: docker pushsif

docker:
	cd docker && docker build --build-arg version=2.12.0 --build-arg num_procs=`grep -c ^proc /proc/cpuinfo` -t blast-ubuntu16:2.12.0 .

sif:
	singularity build blast-ubuntu16_2.12.0.sif docker-daemon://blast-ubuntu16:2.12.0

pushsif:
	singularity sign blast-ubuntu16_2.12.0.sif
	singularity push blast-ubuntu16_2.12.0.sif library://$(SINGULARITY_USER)/default/blast-ubuntu16:2.12.0

clean:
	rm blast-ubuntu16_2.12.0.sif
