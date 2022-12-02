# Aspect Oriented Programming
## What are aspects?
Aspects are code that run before or after method calls, they can read and modify arguments and returns that method provides, and then peform actions based on conditions.

 > AOP is a programming paradigm that aims to increase modularity by allowing the separation of cross-cutting concerns

 It is done by adding additional behavior to existing code without modifying the code itself

Terminologies

 - Join Point: In Spring AOP it always represents a method execution
 - Advice: Action taken by an aspect at a particular join point. Many AOP frameworks model an advice as an interceptor.
 - Pointcut: A predicate that matches join points. Advice is associated with a pointcut expression and runs at any join point matched by the pointcut.
 - Introduction: Declaring additional methods or fields on behalf of a type. Can introduce new interfaces and corresponding implementation to any advised objects.
 - Target object: The object being advised by one or more aspects
 - AOP proxy: An object created by the AOP framework in order to mplement the aspect contracts
 - Weaving: Linking aspects with other application types or objects to create an advised object.

There are different types of advices, `Before`, `After,` `Around`, `AfterThrow`, `AfterReturn`.

 - `Before` runs before the method is called
 - `After` is executed after the method regardless of how the join point exits
 - `AfterThrowing` is executed after the method call throws an error
 - `AfterReturning` is executed after successful completion of the call.
 - `Around` encapsulated the method and can perform action before and after the method call

## Declaring aspects
```java
@Aspect
public class AspectName {

    //Pointcut declaration
    //"execution(<return type> <method name>(<arguments>))" where * can be placed to represent anything. For specific method from packages, can use 'com.bryan.spring.Aop.*' to represent all methods in the Aop class
    // execution(modifiers-pattern? ret-type-pattern declaring-type-pattern? name-pattern(param-pattern) throws-pattern?)

    @Pointcut("execution(* transfer(..))")
    private void pointcutSignature() {

    }

    @Pointcut("within(com.bryan.spring.aop.*)")
    private void withinPointcut

    //joining pointcuts
    @Pointcut("firstPointcutSignature() && secondPointcutSignature()")
    private void combinedPointcut() {

    }
    
    
    //Advice declaration
    @Before("execution(* com.xyz.myapp.dao.*.*(..))")
    public void doAccessCheck() {
        // ...
    }
    
    @AfterReturning(
    pointcut="com.xyz.myapp.SystemArchitecture.dataAccessOperation()", returning="retVal")
    public void doAccessCheck(Object retVal) {
        // ...
    }

    @AfterThrowing(
    pointcut="com.xyz.myapp.SystemArchitecture.dataAccessOperation()",throwing="ex")
    public void doRecoveryActions(DataAccessException ex) {
        // ...
    }

    @Around("com.xyz.myapp.SystemArchitecture.businessService()")
    public Object doBasicProfiling(ProceedingJoinPoint pjp) throws Throwable {
        // start stopwatch
        Object retVal = pjp.proceed();
        // stop stopwatch
        return retVal;
    }
}
```

## Advice ordering
Advice can be ordered to run one before another ddepending on priority when a method has multiple advices tagged to it

## JoinPoint
Pointcuts can be joined together to created comprehensive ways for creating conditions by which advices are executed