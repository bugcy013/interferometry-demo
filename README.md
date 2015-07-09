This is a demo for how to use Jupyter Notebooks and related tools (thebe, tmpnb, Docker, etc) to teach radio interferometry in an interactive format.

# Sample Notebook

Here is the source notebook, [Introduction to Interferometery and Synthesis Imaging](index.ipynb).  You can edit this using the IPython Notebook system.

# Interactive Web Page

You can see an interactive version of the notebook at:

[http://odewahn.github.io/interferometry-demo/public/](http://odewahn.github.io/interferometry-demo/public/)


This page works by converting the raw ipynb file into static HTML, and then using the [thebe](https://github.com/oreillymedia/thebe) plugin to make the code runnable directly in the browser.  (Thebe uses the same JavaScript libraries used in the Jupyter project, but allows you to run the notebook on a different host.) 

It works like this:

* The first time you click "run", thebe starts a Docker container on [tmpnb.org](tmpnb.org) that's running a Jupyter server.  (tmpnb.org is generously supported and maintained by Rackspace.)  Each user gets his or her own container.
* When you click the "Run" button, thebe sends your code to the remote Docker container, which executes it and returns the results.

# Share-cell Examples

[share-cell](https://github.com/rgbkrk/share-cell) is a nice little tool created by Kyle Kelley (@rgbrkr) from Rackspace.  Kyle is a core Jupyter contributor, and is also the creator of tmpnb.  Basically, it just gives you a simple way to share code samples via links.  Here are a few examples from the notebooks above:

* [Fringe frequency](http://odewahn.github.io/interferometry-demo/public/share-cell/?code=%09%0A%23%20Import%20some%20boilerplate%20libraries%0A%25matplotlib%20inline%0Afrom%20IPython.display%20import%20Image%0Afrom%20IPython.html.widgets%20import%20interact%0Afrom%20numpy%20import%20pi%2C%20cos%2C%20sin%0Aimport%20numpy%20as%20np%0Aimport%20pylab%20as%20plt%0Aimport%20seaborn%20as%20sns%0A%0Adef%20plot_fringe(bl_length%2C%20wavelength%2C%20source_spacing)%3A%0A%20%20%20%20%22%22%22%20Plot%20the%20fringe%20function%20for%20a%20baseline%20with%202%20sources%20(see%20Fig%201)%0A%0A%20%20%20%20bl_length%3A%20%20%20%20%20%20distance%20between%20antennas%2C%20in%20m%0A%20%20%20%20wavelength%3A%20%20%20%20%20wavelength%2C%20in%20m%0A%20%20%20%20source_spacing%3A%20distance%20between%20sources%2C%20in%20degrees%0A%20%20%20%20%22%22%22%0A%20%20%20%20theta%20%3D%20np.linspace(-np.pi%2C%20np.pi%2C%20401)%0A%20%20%20%20l%20%3D%20sin(theta)%0A%20%20%20%20l_spc%20%3D%20sin(source_spacing%20%2F%2057.3)%0A%0A%20%20%20%20%23%20first%20baseline%0A%20%20%20%20F_src1_bl1%20%3D%20cos(2%20*%20pi%20*%20bl_length%20*%20l%20%2F%20wavelength)%0A%20%20%20%20F_src2_bl1%20%3D%20cos(2%20*%20pi%20*%20bl_length%20*%20(l%20-%20l_spc)%20%2F%20wavelength)%0A%20%20%20%20F_bl1%20%3D%20F_src1_bl1%20%2B%20F_src2_bl1%0A%0A%20%20%20%20%23%20second%20baseline%0A%20%20%20%20F_src1_bl2%20%3D%20cos(2%20*%20pi%20*%202%20*%20bl_length%20*%20l%20%2F%20wavelength)%0A%20%20%20%20F_src2_bl2%20%3D%20cos(2%20*%20pi%20*%202*%20bl_length%20*%20(l%20-%20l_spc)%20%2F%20wavelength)%0A%20%20%20%20F_bl2%20%3D%20F_src1_bl2%20%2B%20F_src2_bl2%0A%0A%20%20%20%20plt.plot(l%2C%20F_bl1%2C%20c%3D'%23cc0000'%2C%20label%3D%22Baseline%201-2%22)%0A%20%20%20%20plt.plot(l%2C%20F_bl2%2C%20c%3D'%230000cc'%2C%20label%3D%22Baseline%201-3%22)%0A%20%20%20%20plt.xlabel(%22%24sin(%5C%5Ctheta)%24%22)%0A%20%20%20%20plt.ylabel(%22Fringe%20amplitude%22)%0A%20%20%20%20plt.ylim(-2%2C%202)%0A%20%20%20%20plt.legend()%0A%0Af%20%3D%20interact(plot_fringe%2C%20bl_length%3D(1%2C%20100)%2C%20wavelength%3D(1%2C%20100)%2C%20source_spacing%3D(0%2C%2090))%0A%0A&kernel_name=python3)
* [Fringe frequency with multiple sources](http://odewahn.github.io/interferometry-demo/public/share-cell/?code=%09%0A%23%20Import%20some%20boilerplate%20libraries%0A%25matplotlib%20inline%0Afrom%20IPython.display%20import%20Image%0Afrom%20IPython.html.widgets%20import%20interact%0Afrom%20numpy%20import%20pi%2C%20cos%2C%20sin%0Aimport%20numpy%20as%20np%0Aimport%20pylab%20as%20plt%0Aimport%20seaborn%20as%20sns%0A%0Adef%20plot_fringe(bl_length%2C%20wavelength%2C%20source_spacing)%3A%0A%20%20%20%20%22%22%22%20Plot%20the%20fringe%20function%20for%20a%20baseline%20with%202%20sources%20(see%20Fig%201)%0A%0A%20%20%20%20bl_length%3A%20%20%20%20%20%20distance%20between%20antennas%2C%20in%20m%0A%20%20%20%20wavelength%3A%20%20%20%20%20wavelength%2C%20in%20m%0A%20%20%20%20source_spacing%3A%20distance%20between%20sources%2C%20in%20degrees%0A%20%20%20%20%22%22%22%0A%20%20%20%20theta%20%3D%20np.linspace(-np.pi%2C%20np.pi%2C%20401)%0A%20%20%20%20l%20%3D%20sin(theta)%0A%20%20%20%20l_spc%20%3D%20sin(source_spacing%20%2F%2057.3)%0A%0A%20%20%20%20%23%20first%20baseline%0A%20%20%20%20F_src1_bl1%20%3D%20cos(2%20*%20pi%20*%20bl_length%20*%20l%20%2F%20wavelength)%0A%20%20%20%20F_src2_bl1%20%3D%20cos(2%20*%20pi%20*%20bl_length%20*%20(l%20-%20l_spc)%20%2F%20wavelength)%0A%20%20%20%20F_bl1%20%3D%20F_src1_bl1%20%2B%20F_src2_bl1%0A%0A%20%20%20%20%23%20second%20baseline%0A%20%20%20%20F_src1_bl2%20%3D%20cos(2%20*%20pi%20*%202%20*%20bl_length%20*%20l%20%2F%20wavelength)%0A%20%20%20%20F_src2_bl2%20%3D%20cos(2%20*%20pi%20*%202*%20bl_length%20*%20(l%20-%20l_spc)%20%2F%20wavelength)%0A%20%20%20%20F_bl2%20%3D%20F_src1_bl2%20%2B%20F_src2_bl2%0A%0A%20%20%20%20plt.plot(l%2C%20F_bl1%2C%20c%3D'%23cc0000'%2C%20label%3D%22Baseline%201-2%22)%0A%20%20%20%20plt.plot(l%2C%20F_bl2%2C%20c%3D'%230000cc'%2C%20label%3D%22Baseline%201-3%22)%0A%20%20%20%20plt.xlabel(%22%24sin(%5C%5Ctheta)%24%22)%0A%20%20%20%20plt.ylabel(%22Fringe%20amplitude%22)%0A%20%20%20%20plt.ylim(-2%2C%202)%0A%20%20%20%20plt.legend()%0A%0Af%20%3D%20interact(plot_fringe%2C%20bl_length%3D(1%2C%20100)%2C%20wavelength%3D(1%2C%20100)%2C%20source_spacing%3D(0%2C%2090))&kernel_name=python3)
* [Correlator computations](http://odewahn.github.io/interferometry-demo/public/share-cell/?code=from%20IPython.html.widgets%20import%20interact%0Aimport%20numpy%20as%20np%0A%0Atflops_per_gpu%20%3D%201.5%20%20%20%20%20%23%20TFLOP%2Fs%20achievable%20on%20a%20single%20GPU%2C%20NVIDIA%20GTX960%0Acost_per_gpu%20%20%20%3D%20250.0%20%20%20%23%20Cost%20per%20GPU%0A%0Adef%20n_ops(bandwidth%2C%20n_ant)%3A%0A%20%20%20%20n_pol%20%3D%202%0A%20%20%20%20n_antpol%20%3D%20n_ant%20*%20n_pol%0A%20%20%20%20n_baselines%20%3D%20(n_antpol)%20*%20(n_antpol%20%2B%201)%20%2F%202%20%23%20Dual-pol%20%2B%20autocorrelations%0A%20%20%20%20mult_per_sec%20%3D%20n_baselines%20*%20bandwidth%0A%20%20%20%20tflops_per_sec%20%3D%20mult_per_sec%20%20*%205%20%2F%201e6%0A%20%20%20%20n_gpu%20%3D%20np.ceil(tflops_per_sec%20%2F%20tflops_per_gpu)%0A%0A%20%20%20%20to_print%20%3D%20%20%22Bandwidth%3A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%25s%20MHz%5Cn%22%20%25%20bandwidth%0A%20%20%20%20to_print%20%2B%3D%20%22Number%20of%20antennas%3A%20%20%20%20%20%20%20%20%20%20%20%20%25i%5Cn%22%20%25%20n_ant%0A%20%20%20%20to_print%20%2B%3D%20%22Number%20of%20baselines%20(dualpol)%3A%20%25i%5Cn%22%20%25%20n_baselines%0A%20%20%20%20to_print%20%2B%3D%20%22Correlator%20computations%3A%20%20%20%20%20%20%20%252.3f%20TFLOP%2Fs%5Cn%22%20%25%20tflops_per_sec%0A%20%20%20%20to_print%20%2B%3D%20%22Number%20of%20GPUs%20required%3A%20%20%20%20%20%20%20%25i%5Cn%22%20%25%20n_gpu%0A%20%20%20%20to_print%20%2B%3D%20%22Cost%20to%20purchase%3A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%24%25i%22%20%25%20(n_gpu%20*%20cost_per_gpu)%0A%20%20%20%20print(to_print)%0A%0Af%20%3D%20interact(n_ops%2C%20bandwidth%3D(1%2C%201e3)%2C%20n_ant%3D(2%2C%201024))&kernel_name=python3)