# Grails Bootstrap Sample

My Grails 3.0.x sample project with twitter bootstrap and font awesome

Based upon [bootstrap-framework-sample](https://github.com/kensiprell/bootstrap-framework-sample).

## Adjustments to the original code

### Less compiling problems while gradle build

Problem: Asset pipeline tries to compiles not only the bootstrap.less

```
* What went wrong:
Execution failed for task ':assetCompile'.
> java.lang.Exception: LESS Engine Compiler Failed - alerts.less:
   --Could not compile less. 9 error(s) occurred:
  ERROR 10:12 The variable "@alert-padding" was not declared.
    9: .alert {
   10:   padding: @alert-padding;
   11:   margin-bottom: @line-height-computed;
  
  ERROR 11:18 The variable "@line-height-computed" was not declared.
   10:   padding: @alert-padding;
   11:   margin-bottom: @line-height-computed;
   12:   border: 1px solid transparent;
  
  ...
  
  **Did you mean to compile this file individually (check docs on exclusion)?**
```

Solution: Exclude all other less files than the bootstrap.less within teh gradle configuration (build.gradle). 

```
- excludes = ["mixins/*.less"]
+ excludes = ["**/*.less"]
+ includes = ["**/bootstrap.less"]
```