### providedの設定

```gradle
configurations {
    provided
}

sourceSets {
    main.compileClasspath += configurations.provided
    test.compileClasspath += configurations.provided
    test.runtimeClasspath += configurations.provided
}

idea {
    module {
        scopes.PROVIDED.plus += [configurations.provided]
    }
}
```

