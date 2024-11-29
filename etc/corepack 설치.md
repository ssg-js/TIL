# corepack 설치

💡 node 패키지 매니저로 yarn을 사용하기 위해 [공식문서](https://yarnpkg.com/getting-started/install)를 참고해 설치를 진행하다가, corepack enable에 문제가 있어서 기록해두려고 한다. 공식문서는 global로 yarn을 설치하지 말고 프로젝트에 맞춰 패키지 매니저 버전을 관리하기 위해 corepack을 사용하는 걸 권장한다.

> You may notice by reading our [installation guide](https://yarnpkg.com/getting-started/install) that we don't tell you to run `npm install -g yarn` to install Yarn - we even recommend against it. The reason is simple: **just like your project dependencies must be locked, so should be the package manager itself.**

(번역)

> 설치 가이드를 읽어보면 NPM 설치 -g Yarn을 실행하여 Yarn을 설치하도록 지시하지 않으며 심지어 반대할 것을 권장합니다. 그 이유는 간단합니다. 프로젝트 종속성이 잠겨 있어야 하는 것처럼 패키지 관리자 자체도 마찬가지입니다.

출처 : [yarn 공식문서 - corepack](https://yarnpkg.com/corepack)

일단 오류 메세지는 이렇다.

![](corepack%20설치_assets/2024-11-28-11-38-38-image.png)

📕 여기서 EPERM은 "Error Permission"의 약자로 권한이 부족해 작업이 허용되지 않았음을 의미한다. 아래는 EPERM이 발생하는 경우에 대해 정리한 글이다.

> ### Common Scenarios for EPERM Error
> 
> - ****Lack of File System Permissions****: The user running the Node.js process does not have the necessary permissions to write to the specified file or directory.
> - ****File System Restrictions****: The target file or directory may be read-only.
> - ****Operating System Constraints****: System-level restrictions or user account limitations can prevent file operations.
> - ****File Locking****: The file may be locked by another process, preventing write access.
> - ****Special Files****: Attempting to write to system-protected or special files without the required privileges.

(번역)

> ### EPERM 오류의 일반적인 시나리오
> 
> - 파일 시스템 권한 부족: Node.js 프로세스를 실행하는 사용자에게는 지정된 파일이나 디렉토리에 쓰기에 필요한 권한이 없습니다.  
> 
> - 파일 시스템 제한: 대상 파일 또는 디렉토리는 읽기 전용일 수 있습니다.  
> 
> - 운영 체제 제약: 시스템 수준 제한 또는 사용자 계정 제한으로 인해 파일 작업이 차단될 수 있습니다.  
> 
> - 파일 잠금: 다른 프로세스에 의해 파일이 잠겨 있어 쓰기 액세스가 차단될 수 있습니다.  
> 
> - 특수 파일: 필요한 권한 없이 시스템 보호 또는 특수 파일에 쓰기를 시도합니다.

출처 : [How to Solve &quot;File writing permissions blocked by the EPERM&quot; issue in Node.js ? - GeeksforGeeks](https://www.geeksforgeeks.org/how-to-solve-file-writing-permissions-blocked-by-the-eperm-issue-in-node-js/)

(여기서 더하기)

[node.js - nodejs will not enable corepack: operation not permitted - Stack Overflow](https://stackoverflow.com/questions/70577085/nodejs-will-not-enable-corepack-operation-not-permitted)

[GitHub - nodejs/corepack: Zero-runtime-dependency package acting as bridge between Node projects and their package managers](https://github.com/nodejs/corepack#corepack-enable--name)

💡 (문제 상황 or 개요)

📕 (알아본 원인)

> (quote block으로 원문 복사 후 출처 밝히기, 원문 복사 시 원본과 번역본 사이에 (번역) 추가)

출처 : [글 출처](주소)

🔑 (해결방법이나 액션의 결과)

✏ (문제 상황에 대한 최종 해결책 정리 후 마무리)
