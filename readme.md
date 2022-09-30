# See

https://github.com/timkingman/renovate-gradle-bug-20220930 where Renovate doesn't detect a custom Gradle/maven repository.

## My guess was right

This repository has a `build.gradle` that moves the maven repository name after its url, and then Renovate works as I expected, with Renovate failing to find any dependencies, just like Gradle itself does. Renovate doesn't hit maven.apache.org at all.

```
DEBUG: dns lookup error
{
  "host": "repository.timtest.orf",
  "err": {
    "errno": -3008,
    "code": "ENOTFOUND",
    "syscall": "getaddrinfo",
    "hostname": "repository.timtest.orf",
    "message": "getaddrinfo ENOTFOUND repository.timtest.orf",
    "stack": "Error: getaddrinfo ENOTFOUND repository.timtest.orf\n    at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:109:26)"
  }
}
DEBUG: Content is not found for Maven url
{
  "url": "https://repository.timtest.orf/repository/maven-snapshots/org/springframework/spring-webmvc/maven-metadata.xml"
}

...

DEBUG: http statistics
{
  "urls": {
    "https://api.github.com/graphql (POST,200)": 2,
    "https://api.github.com/repos/timkingman/.github/contents/renovate-config.json (GET,404)": 1,
    "https://api.github.com/repos/timkingman/renovate-config/contents/default.json (GET,404)": 1,
    "https://api.github.com/repos/timkingman/renovate-config/contents/renovate.json (GET,404)": 1,
    "https://api.github.com/repos/timkingman/renovate-gradle-bug-20220930-workaround/git/commits (POST,201)": 1,
    "https://api.github.com/repos/timkingman/renovate-gradle-bug-20220930-workaround/git/refs (POST,201)": 1,
    "https://api.github.com/repos/timkingman/renovate-gradle-bug-20220930-workaround/git/trees (POST,201)": 1,
    "https://api.github.com/repos/timkingman/renovate-gradle-bug-20220930-workaround/pulls (GET,200)": 1,
    "https://api.github.com/repos/timkingman/renovate-gradle-bug-20220930-workaround/pulls (POST,201)": 1,
    "https://api.github.com/repos/whitesource/merge-confidence/contents/beta.json (GET,200)": 1,
    "https://repository.timtest.orf/repository/maven-public/org/codehaus/groovy/groovy-json/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-public/org/codehaus/groovy/groovy-test/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-public/org/codehaus/groovy/groovy/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-public/org/springframework/spring-test/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-public/org/springframework/spring-web/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-public/org/springframework/spring-webmvc/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-releases/org/codehaus/groovy/groovy-json/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-releases/org/codehaus/groovy/groovy-test/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-releases/org/codehaus/groovy/groovy/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-releases/org/springframework/spring-test/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-releases/org/springframework/spring-web/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-releases/org/springframework/spring-webmvc/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-snapshots/org/codehaus/groovy/groovy-json/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-snapshots/org/codehaus/groovy/groovy-test/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-snapshots/org/codehaus/groovy/groovy/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-snapshots/org/springframework/spring-test/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-snapshots/org/springframework/spring-web/maven-metadata.xml (GET,0)": 1,
    "https://repository.timtest.orf/repository/maven-snapshots/org/springframework/spring-webmvc/maven-metadata.xml (GET,0)": 1
  },
  "hostStats": {
    "api.github.com": {
      "requestCount": 11,
      "requestAvgMs": 322,
      "queueAvgMs": 0
    },
    "repository.timtest.orf": {
      "requestCount": 18,
      "requestAvgMs": 1,
      "queueAvgMs": 0
    }
  },
  "totalRequests": 29
}
DEBUG: dns cache
{
  "hosts": [
    "api.github.com"
  ]
}
```
