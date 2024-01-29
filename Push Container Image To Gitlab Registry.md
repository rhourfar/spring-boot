# Push Maven Package To Gitlab Repository

add to build.gradle file

{
...

bootBuildImage {
	imageName = System.getenv("CI_REGISTRY_IMAGE") + "/${project.name}:${version}"
  tags = [System.getenv("CI_REGISTRY_IMAGE") + "/${project.name}:latest"]  
  createdDate = "now"
 
	docker {
		publishRegistry {
			username = System.getenv("CI_REGISTRY_USER")
      password = System.getenv("CI_REGISTRY_PASSWORD")
			url = System.getenv("CI_REGISTRY")
		}
	}
}

..
}
