---
Title: "Debugging"
Author: "Kim"
Date: '2014-08-06'
---

***

### Discussion Notes

fatal errors are caused by stop() functions while normal errors were caused by the function not being able to continue

defensive programming's aim is to let you fail fast so you can pinpoint problems as they arise


***

##### Quiz

1. How can you find out where an error occured?

	**`traceback()` should do the job.  Hadley also says binary search.**

1. What does `browser()` do? List the five useful single-key commands
   that you can use inside of a `browser()` environment.
   
   **let's you interactively debug - pauses execution of your commands where the error occurred and lets you investigate the state at that point.
     __ n executes the next step in the function, s is step into which if the next 
    step is a function takes you into that function to work through each line, 
    f finishes execution of the current loop/function, c is for continue which leaves the debugging
     tool and continues regular execution of the function, and q stops debugging and terminates the function to return to the global
      workspace. 'enter' also repeats the previous command and `where` prints the stack trace of active calls (interactive equivalent of traceback)**
   
1. What function do you use to ignore errors in block of code?

	** **

1. Why might you want to create an error with a custom S3 class?

	** **



### Exercises 1

* Compare the following two implementations of `message2error()`. What is the
  main advantage of `withCallingHandlers()` in this scenario? (Hint: look
  carefully at the traceback.)

    ```{r}
    message2error <- function(code) {
      withCallingHandlers(code, message = function(e) stop(e))
    }
    message2error <- function(code) {
      tryCatch(code, message = function(e) stop(e))
    }
    ```


### Exercises 2

* The goal of the `col_means()` function defined below is to compute the means
  of all numeric columns in a data frame.

    ```{r}
    col_means <- function(df) {
      numeric <- sapply(df, is.numeric)
      numeric_cols <- df[, numeric]

      data.frame(lapply(numeric_cols, mean))
    }
    ```

    However, the function is not robust to unusual inputs. Look at
    the following results, decide which ones are incorrect, and modify
    `col_means()` to be more robust. (Hint: there are two function calls
    in `col_means()` that are particularly prone to problems.)

    ```{r, eval = FALSE}
    col_means(mtcars)
    col_means(mtcars[, 0])
    col_means(mtcars[0, ])
    col_means(mtcars[, "mpg", drop = F])
    col_means(1:10)
    col_means(as.matrix(mtcars))
    col_means(as.list(mtcars))

    mtcars2 <- mtcars
    mtcars2[-1] <- lapply(mtcars2[-1], as.character)
    col_means(mtcars2)
    ```

* The following function "lags" a vector, returning a version of `x` that is `n`
  values behind the original. Improve the function so that it (1) returns a
  useful error message if `n` is not a vector, and (2) has reasonable behaviour
  when `n` is 0 or longer than `x`.

    ```{r}
    lag <- function(x, n = 1L) {
      xlen <- length(x)
      c(rep(NA, n), x[seq_len(xlen - n)])
    }
    ```



## Quiz answers {#debugging-answers}

1. The most useful tool to determine where a error occured is `traceback()`.
   Or use Rstudio, which displays it automatically where an error occurs.
   
1. `browser()` pauses execution at the specified line and allows you to
   enter an interactive environment. In that environment, there are five
   useful commands: `n`, execute the next command; `s`, step into the 
   next function; `f`, finish the current loop or function; `c`, continue
   execution normally; `Q`, stop the function and return to the console.
   
1. You could use `try()` or `tryCatch()`.

1. Because you can then capture specific types of error with `tryCatch()`,
   rather than relying on the comparison of error strings, which is risky,
   especially when messages are translated.