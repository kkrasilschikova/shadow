# Minimizing

Shadow can automatically remove all classes of dependencies that are not used by the project, thereby minimizing the resulting shadowed JAR.

```groovy
// Minimizing an shadow JAR
shadowJar {
  minimize()
}
```

A dependency can be excluded from the minimization process thereby forcing its inclusion in the shadow JAR.
This is useful when the dependency analyzer cannot find the usage of a class programmatically, for example if the class
is loaded dynamically via `Class.forName(String)`.

```groovy
// Force a class to be retained during minimization
shadowJar {
  minimize {
    exclude(dependency('org.scala-lang:.*:.*'))
  }
}
```

> Dependencies scoped as `api` will automatically be excluded from minimization and used as "entry points" on minimization.

Similar to dependencies, projects can also be excluded.

```groovy
shadowJar {
    minimize {
        exclude(project(":api"))
    }
}
```

> When excluding a `project`, all dependencies of the excluded `project` are automatically
  excluded as well.
