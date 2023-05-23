---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.5
kernelspec:
  display_name: ir 
  language: ir
  name: ir
---

```{code-cell} r
library("rerddap")
library("ncdf4")
```

```{code-cell} r
?rerddap
```

```{code-cell} r
whichSST <- ed_search(query = "ersstv5")
```

```{code-cell} r
whichSST
```

```{code-cell} r
info('nceiErsstv5_LonPM180')
```

```{code-cell} r
sstInfo <- info('nceiErsstv5_LonPM180')
erSST <- griddap(sstInfo, latitude = c(22., 51.), longitude = c(-140., -105), time = c("2017-01-01", "2017-01-02"), fields = 'ssta')
```

```{code-cell} r
erSST
```

```{code-cell} r
erSST$data
```

```{code-cell} r
urlBase <- "https://gliders.ioos.us/erddap/"
dataInfo <- rerddap::info("allDatasets", url = urlBase)
parameter <- "allDatasets"
```

```{code-cell} r
allGlider <- tabledap(dataInfo)
```

```{code-cell} r
allGlider[0:10,0:3]
```

```{code-cell} r

```
