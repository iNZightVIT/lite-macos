dir <- Sys.getenv("APPDIR")
.libPaths(file.path(dir), "Contents", "Resources", "library")

# Install on first run:
deps <- read.dcf('Contents/Resources/Lite/DESCRIPTION')[, c("Depends", "Imports")]
deps <- as.character(do.call(c, sapply(deps, strsplit, split = ",")))
deps <- trimws(deps)
deps <- deps[!grepl("^R\\s", deps)]
inst <- sapply(deps, requireNamespace, quietly = TRUE)

if (any(!inst)) {
    deps <- deps[!inst]
    r <- tcltk::tkmessageBox(message = 'iNZight Lite needs to install some packages.')
    inzp <- deps[grepl("^iNZight", deps)]
    if (length(inzp)) {
        install.packages(inzp,
            repos = c("https://r.docker.stat.auckland.ac.nz", "https://cran.rstudio.com"),
            dependencies = TRUE
        )
    }
    deps <- deps[!deps %in% inzp]
    install.packages(deps, repos = "https://cran.rstudio.com")
}

shiny::runApp("Contents/Resources/Lite")
