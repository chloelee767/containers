SINGULARITY_USER = lee0767

.PHONY: docker pushsif

docker:
	cd docker && docker build --build-arg VER=3.0.0 --no-cache -t drep_w_mummer-ubuntu16:3.0.0 .

sif:
	singularity build drep_w_mummer-ubuntu16_3.0.0.sif docker-daemon://drep_w_mummer-ubuntu16:3.0.0

pushsif:
	singularity sign drep-ubuntu16_3.0.0.sif
	singularity push drep-ubuntu16_3.0.0.sif library://$(SINGULARITY_USER)/default/drep-ubuntu16:3.0.0

clean:
	rm drep-ubuntu16_3.0.0.sif
