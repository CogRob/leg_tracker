all: help

help:
	@echo ""
	@echo "-- Help Menu"
	@echo ""
	@echo "   1. make build  - build images"
	@echo "   1. make pull   - pull images"
	@echo "   1. make clean  - remove images"
	@echo ""

build:
	@docker build --tag=ros/leg_tracker .

pull:
	@docker pull ros/leg_tracker

clean:
	@docker rmi -f ros/leg_tracker
