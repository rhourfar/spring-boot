# Push Maven Package To Gitlab Repository


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
