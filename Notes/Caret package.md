# [caret package](http://topepo.github.io/caret/index.html)
A wrapper for building and comparing different types of models.  Supports ensembles.  Can be parallelised using either the multicore or cluster models.

```
     modelLookup(model = NULL)
     checkInstall(pkg)
     getModelInfo(model = NULL, regex = TRUE, ...)

     trainControl(method = "boot", number = ifelse(grepl("cv", method), 10, 25),
       repeats = ifelse(grepl("[d_]cv$", method), 1, NA), p = 0.75,
       search = "grid", initialWindow = NULL, horizon = 1,
       fixedWindow = TRUE, skip = 0, verboseIter = FALSE, returnData = TRUE,
       returnResamp = "final", savePredictions = FALSE, classProbs = FALSE,
       summaryFunction = defaultSummary, selectionFunction = "best",
       preProcOptions = list(thresh = 0.95, ICAcomp = 3, k = 5, freqCut = 95/5,
       uniqueCut = 10, cutoff = 0.9), sampling = NULL, index = NULL,
       indexOut = NULL, indexFinal = NULL, timingSamps = 0,
       predictionBounds = rep(FALSE, 2), seeds = NA, adaptive = list(min = 5,
       alpha = 0.05, method = "gls", complete = TRUE), trim = FALSE,
       allowParallel = TRUE)

     ## Default S3 method:
     train(x, y, method = "rf", preProcess = NULL, ...,
       weights = NULL, metric = ifelse(is.factor(y), "Accuracy", "RMSE"),
       maximize = ifelse(metric %in% c("RMSE", "logLoss", "MAE"), FALSE, TRUE),
       trControl = trainControl(), tuneGrid = NULL,
       tuneLength = ifelse(trControl$method == "none", 1, 3))
     
     ## S3 method for class 'formula'
     train(form, data, ..., weights, subset, na.action = na.fail,
       contrasts = NULL)
     
     ## S3 method for class 'recipe'
     train(x, data, method = "rf", ...,
       metric = ifelse(is.factor(y_dat), "Accuracy", "RMSE"),
       maximize = ifelse(metric %in% c("RMSE", "logLoss", "MAE"), FALSE, TRUE),
       trControl = trainControl(), tuneGrid = NULL,
       tuneLength = ifelse(trControl$method == "none", 1, 3))
```

* [List of available Models](http://topepo.github.io/caret/available-models.html)
