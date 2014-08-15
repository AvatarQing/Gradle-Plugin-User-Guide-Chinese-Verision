# Lint support（Lint支持)

> Lint支持，译者注：Lint是一个可以检查Android项目中存在的问题的工具

从0.7.0版本开始，你可以为项目中一个特定的Variant（变种）版本运行lint，也可以为所有Variant版本都运行lint。它将会生成一个报告描述哪一个Variant版本中存在着问题。

你可以通过以下lint选项配置lint。通常情况下你只需要配置其中一部分，以下列出了所有可使用的选项：

    android {
        lintOptions {
            // set to true to turn off analysis progress reporting by lint
            quiet true
            // if true, stop the gradle build if errors are found
            abortOnError false
            // if true, only report errors
            ignoreWarnings true
            // if true, emit full/absolute paths to files with errors (true by default)
            //absolutePaths true
            // if true, check all issues, including those that are off by default
            checkAllWarnings true
            // if true, treat all warnings as errors
            warningsAsErrors true
            // turn off checking the given issue id's
            disable 'TypographyFractions','TypographyQuotes'
            // turn on the given issue id's
            enable 'RtlHardcoded','RtlCompat', 'RtlEnabled'
            // check *only* the given issue id's
            check 'NewApi', 'InlinedApi'
            // if true, don't include source code lines in the error output
            noLines true
            // if true, show all locations for an error, do not truncate lists, etc.
            showAll true
            // Fallback lint configuration (default severities, etc.)
            lintConfig file("default-lint.xml")
            // if true, generate a text report of issues (false by default)
            textReport true
            // location to write the output; can be a file or 'stdout'
            textOutput 'stdout'
            // if true, generate an XML report for use by for example Jenkins
            xmlReport false
            // file to write report to (if not specified, defaults to lint-results.xml)
            xmlOutput file("lint-report.xml")
            // if true, generate an HTML report (with issue explanations, sourcecode, etc)
            htmlReport true
            // optional path to report (default will be lint-results.html in the builddir)
            htmlOutput file("lint-report.html")

       // set to true to have all release builds run lint on issues with severity=fatal
       // and abort the build (controlled by abortOnError above) if fatal issues are found
       checkReleaseBuilds true
            // Set the severity of the given issues to fatal (which means they will be
            // checked during release builds (even if the lint target is not included)
            fatal 'NewApi', 'InlineApi'
            // Set the severity of the given issues to error
            error 'Wakelock', 'TextViewEdits'
            // Set the severity of the given issues to warning
            warning 'ResourceAsColor'
            // Set the severity of the given issues to ignore (same as disabling the check)
            ignore 'TypographyQuotes'
        }
    }
