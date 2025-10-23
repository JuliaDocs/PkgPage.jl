<!-- =============================
     ABOUT
    ============================== -->

\begin{section}{title="About this Package", name="About"}

\lead{PkgPage.jl is based upon [Franklin.jl](https://github.com/JuliaDocs/Franklin.jl) and makes it easy to create a beautiful landing page for a package in less than 10 minutes.}

PkgPage uses [Bootstrap 4.5](https://getbootstrap.com/docs/4.5/getting-started/introduction/) and is meant to be particularly easy to use with minimal need to tweak HTML or CSS to get a great-looking result.
With it you can:

* easily insert and style figures and tables,
* easily initiate a multi-columns environment,
* easily control the layout, colors, code theme etc from the config file,
* automatic insertion of new sections into the navbar,
* automatic purging of bootstrap css to remove unused rules,
* all the goodies from [Franklin.jl](https://github.com/JuliaDocs/Franklin.jl):
    * live-rendering,
    * support for [KaTeX](https://github.com/KaTeX/KaTeX) and [highlight.js](https://highlightjs.org/) and automatic pre-rendering,
    * and [much more](https://franklinjl.org/).

\end{section}


<!-- ==============================
     GETTING STARTED
     ============================== -->
\begin{section}{title="Getting started"}


In order to get started, just add the package (with **Julia ≥ 1.3**) and

```julia-repl
julia> using PkgPage
julia> newpage()
julia> serve()
```

\\

The `newpage` call will
* generate a `page/` folder in your current directory which contains all the material to generate your site,
    * modify `page/config.md` to change the description, layout, colors etc.,
    * modify `page/index.md` to change the content.
* place a `.github/workflows/DeployPage.yml` to enable the github action that will help deploy your page.

The `serve` call will render your page and make it available for live-preview in your browser when you make modifications to either `config.md` or `index.md`.

\alert{You can specify another folder name via `newpage(path="page2")` but don't forget to modify this in the `DeployPage.yml` as well (in 2 spots).}

\end{section}



<!-- ==============================
     SPECIAL COMMANDS
     ============================== -->
\begin{section}{title="Commands"}

\lead{PkgPage makes a few special commands available to you to simplify the insertion of common useful environments.
}

* [Sections](#com-sections)
* [Figures](#com-figures)
* [Tables](#com-tables)
* [Columns](#com-columns)
* [Maths](#com-maths)
* [Misc](#com-misc)

\label{com-sections}
**Sections**: you can indicate a section as follows:

```plaintext
\begin{section}{opts...}
text
\end{section}
```

where the available options are:

* `title="..."` to add a heading to the section, this should be provided,
* `name="..."` to add a specific name that will appear in the navbar (if not given, it will use the given title).
* `width=8` an integer number controlling the width of the section with respect to the body, increase it to get a wider section.
\label{com-figures}
**Figures**: you can indicate a figure as follows:

```plaintext
\figure{path="...", opts...}
```

where `path` is a valid path to the image (e.g. `/assets/image.png`) and the other available options are:

* `width="..."` to specify the width of the image (e.g. `100%`),
* `alt="..."` to specify the image `alt`,
* `caption="..."` to specify the figure caption if any,
* `style="..."` to add any specific CSS styling to the image (e.g. `border-radius:5px`).

**Note**: `alt` and `caption` are passed as HTML strings so, for instance, if you want a line break you will need to use `<br>` or if you want maths in the caption you will need to put it between escaped brackets `\(x^2\sin(\mu)\)` instead of `$`.

\begin{center}
  \figure{
    path="/assets/nice_image.jpg", width="100%", style="border-radius:5px;",
    caption=raw"Panoramic view of the Tara Cathedrals (taken from Wikimedia). <br>(Note: maths can be used in caption but between brackets: \(x^2\sin(\mu)\))."
  }
\end{center}

\label{com-tables}
**Tables**: you can insert a table as follows:

```plaintext
\begin{table}{opts...}
| Column One | Column Two | Column Three |
|----------: | ---------- |:------------:|
| Row `1`    | Column `2` |              |
| *Row* 2    | **Row** 2  | Column ``3`` |
\end{table}
```

where the available options are:

* `caption="..."`: to add a caption to the table,
* `class="..."`: to add specific bootstrap classes to the table (e.g. `table-striped`),
* `style="..."`: for any further styling.

\begin{center}
\begin{table}{caption="A simple table", class="table-striped"}
| Column One | Column Two | Column Three |
|:---------- | ---------- |:------------:|
| Row `1`    | Column `2` |              |
| *Row* 2    | **Row** 2  | Column ``3`` |
\end{table}
\end{center}

\label{com-columns}
**Columns**: you can declare an environment with columns with:

```plaintext
\begin{columns}
\begin{column}{}
...
\end{column}
\begin{column}{}
...
\end{column}
\end{columns}
```

For instance you can use this to produce:

\begin{columns}
\begin{column}{}
**_Content of a first column here_**

Here is some more content for that first column.
\end{column}
\begin{column}{}
**_Content of a second column here_**

Here is some more content for that second column.
\end{column}
\end{columns}

\\

\label{com-maths}
**Maths**

Just use `$$ ... $$` for display math and  `$ ... $` for inline maths:

$$ w_i = {2 \over (1-x_i^2)[P'_n(x_i)]^2} $$ <!--_-->

where $P_n$ is the $n$-th [Legendre polynomial](https://en.wikipedia.org/wiki/Legendre_polynomials) and $x_i$ is it's $i$-th root.

\label{com-misc}
**Misc**

* you can use `\\` to add some vertical space (skip a line)
\\
* you can use `\begin{center}...\end{center}` to center some content
\begin{center}
_some centered content_
\\\\
\end{center}
* you can use `\style{css}{content}` to get css-styled text for instance `\style{color:red;text-transform:uppercase;}{hello}` gives \style{color:red;text-transform:uppercase;}{hello}
* you can use `\alert{...}` to draw attention to some text via a coloured box.

\alert{this is an alert}

You can also define your own commands which can be as complex as you might want, see the [Franklin docs](https://franklinjl.org) for more information.

\end{section}


<!-- =============================
     SHOWING CODE
    ============================== -->

\begin{section}{title="Showing Code"}

\lead{
    Franklin can run your Julia code on the fly and show the output.
}

**Setting up the environment**: the first step is to ensure that the folder with your source has the proper environment including your package.
To do so, in the Julia REPL, navigate to the source (e.g. `cd("page/")`), activate the environment (e.g. `using Pkg; Pkg.activate()`) and add the package(s) that you need (e.g. `Pkg.add("DataFrames")`).
If you check the status or the Project.toml, you will see that `Franklin` is already in there on top of whatever packages you might have chosen to add.
In our current case:

```
Status `~/.julia/dev/PkgPage/page/Project.toml`
  [a93c6f00] DataFrames v0.21.2
  [713c75ef] Franklin v0.8.2
```

Also add the package in the `DeployPage.yml` e.g. in our case there is:

```julia
Pkg.add(["NodeJS", "DataFrames"]);
```

Once that's set up, you can use "named" code blocks i.e. code blocks that look like

`````
```julia:ex
using DataFrames
df = DataFrame(A = 1:4, B = ["M", "F", "F", "M"])
first(df, 3)
```
`````

where `:ex` is the "named part" (`ex` being the name, which should be unique on the page).

```julia:ex
using DataFrames
df = DataFrame(A = 1:4, B = ["M", "F", "F", "M"])
first(df, 3)
```

You can control the indentation and appearance of the output block in the `config.md` too.

\end{section}


<!-- =============================
     Deploying
    ============================== -->

\begin{section}{title="Deployment"}

\lead{Make your page available online easily by leveraging GitHub Actions and GitHub Pages.}

By following these instructions, the content of the rendered website will be copied to a `gh-pages` branch where it will be deployed by GitHub.
If you would like to deploy the page with your own URL or using something else than GitHub, have a look at the specific instructions further on.

**Adjust DeployPage**: start by checking the `.github/workflows/DeployPage.yml` in particular:
* if you want to use Python or matplotlib, uncomment the relevant lines
* in the `run` block ensure that
    * `NodeJS` and `PkgPage` are added,
    * any packages that your page might rely on are added,
    * the `optimize` call has the appropriate `input` and `output` path (if you're in the default setting, leave as is).

**GitIgnore**: it's important you specify that `page/__site` should be ignored by git and not pushed to your repository otherwise the build process might not work properly. To do so create a file `.gitignore` containing the line

```
page/__site
```

as shown [here](https://github.com/JuliaDocs/PkgPage.jl/blob/cce098535eb95c2c3ba919d605792abfee57710c/.gitignore#L3).

**GitAttributes**: in order for GitHub to ignore `page` folder it the language statistics for your repository, make sure to add a file `.gitattributes` with content

```
page/* linguist-vendored
```

like [this](https://github.com/JuliaDocs/PkgPage.jl/blob/master/.gitattributes).

Now whenever you push changes to the `master` branch of your package, the  build process will be triggered and your page updated and deployed.
**That's it**.

**Avoiding clashes with Documenter.jl**: if you already use [Documenter.jl](https://github.com/JuliaDocs/Documenter.jl) you might want your page to be deployed in a specific folder of `gh-pages` as Documenter also generates files in `gh-pages`.

\alert{This will typically not be necessary as the names created by PkgPage and Documenter don't clash, but you might still prefer to avoid mixing the two (in which case, read on).}

you can do so in two steps:

1. change the `run` part of `DeployPage.yml` by specifying the `output` keyword argument  in `PkgPage.optimize` for instance: `PkgPage.optimize(input="page", output="page")`,
1. change the `prepath` in `config.md` to reflect that the base URL will contain that additional folder, for instance `@def prepath = "YourPackage.jl/page"`.

**Use your own URL**: you can usually get host services like Netlify to deploy a specific branch of a GitHub repo, do make sure to set `@def prepath = ""` in your `config.md` though.

If you want to do the deployment without GitHub actions then you will need to:

* ensure you have `purgecss` and `highlights` installed and available to `NodeJS`, the simplest way to do this is to install them via `NodeJS` with

```
using NodeJS;
run(`$(npm_cmd()) install highlight.js`);
run(`$(npm_cmd()) install purgecss`);
```
\\
* run `PkgPage.optimize(input="page", output="")` (adapting `input` as required)
* place the content of `page/__site` wherever your server requires it.

\end{section}
