## 1. installing mason cli
```
dart pub global activate mason_cli
```
## 2. initializing mason workspace
```
mason init
```
## 3. creating a new brick called 'test'
```
mason new test
```
## 4. generating mason brick
``` 
mason generate test 
```
## 5. adding templates -> site: `brickhub.dev`
```
mason add test
```
## 6. creating custom brick
Note: put your folders inside __brick__ that get generated.
## 7. adding brick to local 'test'
```
mason add test --path 'path/to/brick'
```
## 8. adding brick to global
```
mason add test --path 'path/to/brick' --global
```
### Notes
        - note brick version with `mason list`
        - go to `/Users/"name"/.mason-cache`.
        - move brick to `/hosted/registry.brickhub.dev`
        - change what inside `global` to everything to brick added with new path.
### OR
        - go to `Users/"name"/.mason-cache/hosted/registry.brickhub.dev`.
        - add brick add blank brick directly, then change it as you want.
