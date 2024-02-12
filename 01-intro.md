# Introduction 

## Container 
	
    A Generic Wrapper for Application.

	It contains App with All of its dependencies
	Dependencies:
		Langauge SDK, Server Runtime, Third Party Libs and Base OS Libs

## Container Runtime:
	A Small environment to run containers.
	Examples: libcontainerd, cri-o, docker & podman

## Container SDK / Development Environment:
	
    A Complete SDK for Building, Running and Debugging containers
	Example: Docker & Podman

## Docker 
	
    Container SDK / Dev Environment which provides support for Both Linux and Windows.
	
## Earlier (Legacy) Container Runtimes:
	
    - RedHat has a built in container runtime "LXC" (OS Containers)
	- Debian has a built in container runtime "LXD" (OS Containers)

	Legacy OS Containers allowed running complete "LINUX" system in another Host Linux system without any Hypervisor !



## Container Image:
	
    A Readyonly "Template" for containers. Has all the dependencies + metadata (JSON) + Execution instructions

## Container Instance:

	Actual instance from Image, consumes CPU,RAM, Storage and Network !
	Has IP Address assigned.

## Container Image Registry 

    A Remote Service that manages container images, also provide secure method (RBAC) to authorize push/pull of images.

### Public Registry

    Container Registy accessible to general public. Any one can `pull` images without signup.

    Examples : 
    
    - Docker Registry ( Accessible from https://hub.docker.com )
    - Microsoft Public Registry ( mcr.microsoft.com )

### Private Self Hosted Registries

    Container registries hosted on on-premise servers, managed by internal team. Not accessible to outside world.
    
    Example:

    - JFrog Container registry

### Private Cloud Registry

    Container registries hosted on any cloud platform. 

    Example:

    - Azure Container Registry (ACR)
    - Elastic Container Registry (ECR)

