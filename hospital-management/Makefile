SERVICES = directory-service case-service patient-service appointment-service api-gateway
DOCKER_REPO = vaish864

all: clone git_status git_pull git_stash build_lib build_services build_images  push_images

clone:
	@echo "Cloning all services and JavaFX project..."
	@for service in $(SERVICES); do \
		if test ! -d $$service; then \
			git clone https://github.com/vaishnavimatre/makefile-learn.git temp_repo; \
		else \
			echo "$$service already exists."; \
		fi \
	done

git_status:
	@echo "Getting git status for all projects..."
	@for project in $(SERVICES) ; do \
		if test -d $$project; then \
			(cd $$project && git status); \
		else \
			echo "Directory $$project does not exist."; \
		fi \
	done

git_pull:
	@echo "Pulling latest changes for all projects..."
	@for project in $(SERVICES) ; do \
		if test -d $$project; then \
			(cd $$project && git pull); \
		else \
			echo "Directory $$project does not exist."; \
		fi \
	done

git_stash:
	@echo "Stashing changes in all projects..."
	@for project in $(SERVICES); do \
		if test -d $$project; then \
			(cd $$project && git stash); \
		else \
			echo "Directory $$project does not exist."; \
		fi \
	done


build_services:
	@echo "Building all services..."
	@for service in $(SERVICES); do \
		if test -d $$service; then \
			(cd $$service && mvn clean package); \
		else \
			echo "Directory $$service does not exist."; \
		fi \
	done

build_images:
	@echo "Building Docker images for all services..."
	@for service in $(SERVICES); do \
		if test -d $$service; then \
			docker build -t $(DOCKER_REPO)/$$service:latest $$service; \
		else \
			echo "Directory $$service does not exist."; \
		fi \
	done

push_images: 
	@echo "Pushing all Docker images..."
	@for service in $(SERVICES); do \
		docker push $(DOCKER_REPO)/$$service:latest; \
	done



