# Push Maven Package To Gitlab Repository



## Push Package To Maven Repository
add to build.gradle

```
publishing {
	publications {
		bootJava(MavenPublication) {
			artifact tasks.named('jar')
		}
	}
	repositories {
		maven {
			name = 'GitLab'
			url = System.getenv("CI_API_V4_URL") + '/projects/' + System.getenv("CI_PROJECT_ID") + '/packages/maven'
			credentials(HttpHeaderCredentials) {
				name = 'JOB-TOKEN'
				value = System.getenv("CI_JOB_TOKEN")
			}
			authentication {
				header(HttpHeaderAuthentication)
			}
		}
	}
}
```


## Pull Package From Maven Repository
add to build.gradle
```
repositories {
	maven { 
           url "${gitlab_repo}"
	    name 'Gitlab'
	    credentials(HttpHeaderCredentials) {
	      name = "${gitlab_token_name}"
	      value = "${gitlab_token_value}"
	    }
	    authentication {
	      header(HttpHeaderAuthentication)
	    }	    
     }
	  mavenCentral()
	  maven { url 'https://artifactory-oss.prod.netflix.net/artifactory/maven-oss-candidates' }
}
```

add to gradle.properties

gitlab_repo=https://**YOUR Gitlab URL**/api/v4/groups/**Group Id**/-/packages/maven
or
gitlab_repo=https://**YOUR Gitlab URL**/api/v4/projects/**Project Id**/-/packages/maven

gitlab_token_name=Deploy-Token
gitlab_token_value=**YOUR_TOKEN**


how to create deploy token
https://docs.gitlab.com/ee/user/project/deploy_tokens/
