# Luna: parallel scans from notebook.

For running [Luna.jl](https://github.com/LupoLab/Luna.jl) jobs/[scans in parallel](http://lupo-lab.com/Luna.jl/stable/scans.html#Parameter-scans) from [Jupyter/IJulia notebooks](https://julialang.github.io/IJulia.jl/stable/).


**UPDATE NOV 2023**

The issue with running Luna scans directly from Jupyter/IJulia can be fixed with the workaround from https://github.com/LupoLab/Luna.jl/issues/317 - see the demo notebook [demo/luna_scan_demo_271123.ipynb](https://github.com/phockett/Luna.jl-jupyterDispatch/blob/main/demo/luna_scan_demo_271123.ipynb) for a basic working example.


---

**What and why**

Jupyter is great, and I like to do everything in/from a notebook... but dispatching [Luna.jl](https://github.com/LupoLab/Luna.jl) jobs/[scans in parallel](http://lupo-lab.com/Luna.jl/stable/scans.html#Parameter-scans) from a notebook was buggy and inconsistent when I tried it. (UPDATE: it seems that the issue is due to the way IJulia wraps system calls, for more discussion see [Luna.jl #317](https://github.com/LupoLab/Luna.jl/issues/317).)

Instead of running jobs directly, this template writes a job file, then dispatches that to a parallel Julia pool via a shell script. Each set of results is put in a separate dir, along with output figures, for later inspection.


**Notes**

- To function, this requires a working [IJulia installation](https://julialang.github.io/IJulia.jl/stable/), and [Luna.jl](https://github.com/LupoLab/Luna.jl) - these can be installed via `using Pkg; Pkg.add("IJulia"); Pkg.add("Luna")`. For the final image display cell, you may also need `import Pkg; Pkg.add("Images"); Pkg.add("FileIO")`.
- The job template is lifted [more-or-less directly from the Luna.jl parameter scan docs](http://lupo-lab.com/Luna.jl/stable/scans.html#Parameter-scans), except with the addition of multi-mode handling (per [Luna.jl #316](https://github.com/LupoLab/Luna.jl/issues/316)).
- The parallel jobs are detached from the notebook, so should persist until completed, even at notebook close/disconnect.
- Tested in Julia v1.8.5, IJulia v1.24.0, Luna v0.2.0. 
- Additional notes in notebook.
- For Docker builds, see [Open Photoionization Docker Stacks](https://github.com/phockett/open-photoionization-docker-stacks/tree/main/luna).


**Instructions**

See the `scan_parallel_Luna_template.ipynb` notebook.
