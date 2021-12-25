
##### 스페이스 치환 #1

```
rename ' ' '_' *
```

##### 스페이스 치환 #2
```
find * -type f -name "* *" -exec rename "s/\s/_/g" {} \;
```

##### 스페이스 치환 #3
```
find . -type f -name "* *" -print0 -exec bash -c ‘mv "$0" "${0// /_}"’ {} \;
```

##### mp3 file 확인
```
find . -name "*.mp3" -exec bash -c "basename \"{}\" && file \"{}\" | awk -F: '{\$1=\"\"; print \$0 }'" \;
```

##### inode-number 로 파일 찾기
```
find . -inum 13792273859331238 -exec file {} \;
```

##### awk 기본 문법
```
echo "Hello Tom" | awk '{$2="Adam"; print $0}'
```
