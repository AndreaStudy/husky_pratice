# eslint + prettier + husky 시작하기

1. next install 하기
   
   - npx create-next-app@latest .
   
   

2. eslint, prettier install 하기
   
   - npm install --save-dev --save-exact prettier
   - npm install --save-dev eslint-config-prettier
   
   

3. prettier configuration update
   
   - .prettierrc.json (기본 설정하는 파일)
   - .prettierignore (설정 무시하는 파일 설정)
   
   

4. prettier extenstion install 하기 
   
   - prettier - code formatter install(vscode extension)
   
   

5. prettier extenstion 설정(안해도 됨.)
   
   - formatter on Save (저장할 때 자동 포매팅)
   
   

6. husky install
   
   - npx husky-init && npm install
   
   

7. add pre-commit
   
   - npx husky add .husky/pre-commit "npx lint-staged"
   
   

8. install lint-staged
   
   - npm i -D lint-staged
     
     ```json
     // add pacckage.json
     "lint-staged": {
     "*.{js,jsx,ts,tsx,css,scss}": [
      "prettier --write",
      "eslint --fix"
     ]
     },  
     ```

9. add commit-msg
   
   - npx husky add .husky/commit-msg
   
   

10. modify commit-msg

```
#!/bin/sh
. "$(dirname -- "$0")/_/husky.sh"

message="$(cat $1)"
requiredPattern="^(:[\w-]+:)(init|feat|test|fix|docs|style|refactor|perf|build|ci|chore|revert): .+$"

# Use grep with Perl-compatible regex for emoji support
if ! echo "$message" | grep -Pq "$requiredPattern"; then
  echo "=========================================================================="
  echo "======================   🚨 WRONG COMMIT MESSAGE!   ======================"
  echo "=========================================================================="
  echo "== Format should be => [emoji][type]: [subject]                         =="
  echo "== Allowed Types: init, feat, test, fix, docs, style, refactor, perf, build, ci, chore, revert =="
  echo "== EXAMPLE => :emoji_name:feat: Add new feature                         =="
  echo "=========================================================================="
  echo "== Your commit message was => $message "
  echo "== For more information, check script in .husky/commit-msg or README.md =="
  echo "=========================================================================="
  exit 1
else
  echo "=========================================================================="
  echo "=======================      COMMIT CREATED!!      ======================="
  echo "=========================================================================="
fi
```