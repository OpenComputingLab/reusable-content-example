# Thebe-lite demo

We can use [thebe-lite](https://mystmd.org/thebe/quickstart-lite) to make code executable within a page.

```{figure} images/thebe-lite.png
:name: thebe_lite_preview
:width: 400px

Screenshot or Thebe-Lite widget.
```

Embed the executable code widget using an admonition of the form:

````text
```{ou-codestyle} python
:type: thebelite
# We can install packages
%pip install matplotlib

# Print a message
print("hello")

#Return an object as the final line
message = "Hello"

message
```
````

When activated, the code is editable and executable. If the last line returns an object, the object is displayed.

Example of using thebe-lite to run an interactive widget with a `xeus-python` JupyterLite kernel:

```{ou-codestyle} python
:type: thebelite

%pip install ipywidgets==8.0.7
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

from ipywidgets import interact, interactive
from IPython.display import clear_output, display, HTML

import numpy as np
from scipy import integrate

from matplotlib import pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from matplotlib.colors import cnames
from matplotlib import animation

def solve_lorenz(
  N=10, angle=0.0, max_time=4.0, 
  sigma=10.0, beta=8./3, rho=28.0):

    fig = plt.figure()
    ax = fig.add_axes([0, 0, 1, 1], projection='3d')
    ax.axis('off')

    # prepare the axes limits
    ax.set_xlim((-25, 25))
    ax.set_ylim((-35, 35))
    ax.set_zlim((5, 55))
    
    def lorenz_deriv(x_y_z, t0, sigma=sigma, beta=beta, rho=rho):
        """Compute the time-derivative of a Lorenz system."""
        x, y, z = x_y_z
        return [sigma * (y - x), x * (rho - z) - y, x * y - beta * z]

    # Choose random starting points, uniformly distributed from -15 to 15
    np.random.seed(1)
    x0 = -15 + 30 * np.random.random((N, 3))

    # Solve for the trajectories
    t = np.linspace(0, max_time, int(250*max_time))
    x_t = np.asarray([integrate.odeint(lorenz_deriv, x0i, t)
                      for x0i in x0])
    
    # choose a different color for each trajectory
    colors = plt.cm.viridis(np.linspace(0, 1, N))

    for i in range(N):
        x, y, z = x_t[i,:,:].T
        lines = ax.plot(x, y, z, '-', c=colors[i])
        plt.setp(lines, linewidth=2)

    ax.view_init(30, angle)
    plt.show()

    return t, x_t

w = interactive(solve_lorenz, angle=(0.,360.), max_time=(0.1, 4.0), 
                N=(0,50), sigma=(0.0,50.0), rho=(0.0,50.0))
display(w)
```

The widget may need resizing to display the output. The *Resize* button provides a manual way of doing this. Ideally, we would resize the window by observing an event [[docs](https://github.com/executablebooks/thebe/blob/main/apps/docs/events.rst)] that shows the output area has been updated or the run command has finished.

## ISSUES

Thebe-lite is intended to be deplyed at the top level of a page. When activated, it makes all code cells executable. TO be used in this way requires modifications to be made to the VLE course content page template. Instead, the demo loads the code and thebe-lite application into an iframe using an HTML5.zip bundle. This means that if multiple code items are included in the same page, *separate* instances of thebe-lite are loaded in and there is no communication bewteen them. If thebe-lite were loaded in at the top level of the page, code executed in one block would affect the Pyhton state available to code blocks elsehwere in the same page.