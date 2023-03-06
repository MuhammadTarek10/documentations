## installing mason cli
    `dart pub global activate mason_cli`
## initializing mason workspace
    `mason init`
## creating a new brick called 'test'
    `mason new test`
## creating custom brick
    put your folders inside __brick__ that get generated.
## adding brick to local 'test'
    `mason add test --path 'path/to/brick'`
## adding brick to global
    `mason add test --path 'path/to/brick' --global`
        Notes:
            - note brick version with `mason list -g`
            - go to `/Users/"name"/.mason-cache`.
            - move brick to `/hosted/registry.brickhub.dev`
            - change what inside `global` to everything to brick added with new path.
    OR
        - go to `Users/"name"/.mason-cache/hosted/registry.brickhub.dev`.
        - add brick add blank brick directly, then change it as you want.
