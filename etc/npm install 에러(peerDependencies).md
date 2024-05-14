# npm install 에러(peerDependencies)

💡 예전에 과제 테스트를 쳤던 프로젝트를 다시 풀어보고자 클론 받은 후 npm install을 하려다 보니 오류가 생겼다. 해결하는 과정에서 배울 게 있을 것 같아서 기록해보려고 한다!

오류 메세지는 이렇다.

![](npm%20install%20에러_assets/2024-04-27-00-59-15-image.png)

해당 오류 정보에서는 msw "1.2.1" 을 설치하는 도중에 typescript 5.1.6 에서 문제가 발생했다고 나와있다.

난 그래서 typescript를 강제로 설치하면 되지 않을까 생각했지만, 그래도 이를 계기로 에러 상황에 대해 공부해보려고 한다.

📕 이는 2021년 2월 출시된 npm 7버전부터 **peerDependencies를 자동으로 설치하는 기능** 때문이다.

> ### Peer dependencies
> 
> Automatically installing peer dependencies is an exciting new feature introduced in npm 7. In previous versions of npm (4-6), peer dependencies conflicts presented a warning that versions were not compatible, but would still install dependencies without an error. npm 7 will block installations if an upstream dependency conflict is present that cannot be automatically resolved.
> 
> You have the option to retry with `--force` to bypass the conflict or `--legacy-peer-deps` command to ignore peer dependencies entirely (this behavior is similar to versions 4-6).
> 
> Since many packages in the ecosystem have come to rely on loose peer dependencies resolutions, npm 7 will print a warning and work around most peer conflicts that exist deep within the package tree, since you can’t fix those anyway. To enforce strictly correct peer dependency resolutions at all levels, use the `--strict-peer-deps` flag.

(번역)

> 피어 종속성을 자동으로 설치하는 것은 npm 7에서 도입된 흥미로운 새로운 기능입니다. 이전 버전의 npm(4-6)에서 피어 종속성 충돌은 버전이 호환되지 않지만 여전히 오류 없이 종속성을 설치한다는 경고를 제공했습니다. 자동으로 해결할 수 없는 업스트림 종속성 충돌이 있는 경우 npm 7은 설치를 차단합니다.  
> 
> --force를 사용하여 충돌을 우회하거나 --legacy-peer-deps 명령을 사용하여 피어 종속성을 완전히 무시할 수 있습니다(이 동작은 버전 4-6과 유사).  
> 
> 생태계의 많은 패키지가 느슨한 피어 의존성 해결책에 의존하게 되었기 때문에 npm 7은 경고를 출력하고 패키지 트리의 깊은 곳에 존재하는 대부분의 피어 충돌을 해결합니다. 모든 수준에서 엄격하게 올바른 피어 의존성 해결책을 적용하려면 --strict-peer-deps 플래그를 사용하십시오.

출처 : [npm 7 is now generally available! - The GitHub Blog](https://github.blog/2021-02-02-npm-7-is-now-generally-available/)

위 글을 보면 npm 4-6버전에서는 버전이 맞지 않을 경우 경고만 표기하고 에러 없이 설치했다고 되어있다. 하지만 npm 7버전은 업스트림(?) 종속성 충돌이 발생하면 설치를 차단한다.

이 문제는 에러 메시지 중후반에 나와있는 `--force` 나 `--legacy-peer-deps` 속성을 이용해 설치하면 해결할 수 있다.

> 둘 중에 뭐가 나은지는 의견이 분분한데 한국 블로그에선 대부분 `--force`를 사용하고 있고, stack overflow에서는 `--legacy-peer-deps`가 낫다는 의견이 많은 것 같다. 
> 개인적으로는 npm 4-6버전과 동일하게 동작한다는 `--legacy-peer-deps`가 나아보인다. --force의 경우 이전 npm 4-6버전에서 동작과 달리 강제로 우회하면서 또 다른 문제가 발생하지 않을까 생각되기 때문이다.

🔑 아무튼 `npm install --legacy-peer-deps`로 설치하면 무수한 경고와 함께 설치가 진행된다.

![](npm%20install%20에러_assets/2024-05-15-01-52-54-image.png)

그리고 친절하게 현재 단계별 취약점과 해결방법을 알려준다.

![](npm%20install%20에러_assets/2024-05-15-01-54-42-image.png)

🔑 `npm audit`은 현재 취약한 부분에 대한 정보를 알려준다.

> The audit command submits a description of the dependencies configured in your project to your default registry and asks for a report of known vulnerabilities. If any vulnerabilities are found, then the impact and appropriate remediation will be calculated.

(번역)

> audit은 프로젝트에 구성된 종속성에 대한 설명을 기본 레지스트리에 제출하고 알려진 취약성에 대한 보고서를 요청합니다. 취약성이 발견되면 영향과 적절한 복구가 계산됩니다.

출처 : https://docs.npmjs.com/cli/v7/commands/npm-audit

심각도가 적당한 부분도 나오고,

![](npm%20install%20에러_assets/2024-05-15-02-02-18-image.png)

critical하거나 high인 부분도 나온다.

![](npm%20install%20에러_assets/2024-05-15-02-03-00-image.png)

![](npm%20install%20에러_assets/2024-05-15-02-03-12-image.png)

🔑 이제 해결하기 위해 `npm audit fix`를 실행하면, 

![](npm%20install%20에러(peerDependencies)_assets/2024-05-15-02-15-07-image.png)

🔑 또 에러가 뜨기 시작한다.. 이 에러들을 하나하나 잡는건 너무 많이 시간과 노력이 들 것 같아서(사실 불가능해 보인다) 바로 npm audit을 알려준(위 x 5번째 사진) 메세지에 나와있는 `npm audit fix --force`를 실행했다.

하지만, 아무리 계속해도 취약점이 줄지않았다.. 하지만 이렇게 넘기긴 넘 찝찝해서 더 서칭해봤다.

[npm audit으로 보안취약점을 발견했을 때의 조치 - Never test](https://lovemewithoutall.github.io/it/npm-audit-fix/)
