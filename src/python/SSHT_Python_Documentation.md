# SSHT Python Documentation

This guide is intended to explanin the python interface of SSHT. For a description of the workings of SSHT see [here](http://astro-informatics.github.io/ssht/ "SSHT documentation")

## pyssht.forward

~~~~{.python}
flm = pyssht.forward(f, int L, Spin=0, Method='MW', Reality=False)
~~~~

Performs the forward spherical harmonic transform.

#### Inputs

* `f` the signal on the sphere, `numpy.ndarray` type `complex` or `real`, ndim 2. NB different for `'MW_pole'` sampling.
* `L` the band limit of the signal, non-zero positive integer
* `Spin` the spin of the signal, non-negative integer (default = 0)
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    2. `'MW_pole'`    [McEwen & Wiaux sampling with the south pole as a seperate double.]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]
* `Reality`  determines if the signal is real or complex, Boolian (default = False)

#### Output

`flm` the spherical harmonic transform of `f`, 1D `numpy.ndarray` type `complex`

#### Note on `'MW_pole'` sampling

This is the same as the `'MW'` sampling however the south pole is expessed as a double only not a vector. Therefore the size of the array is one smaller on the \(\theta\) direction. `f` is now a tuple containing either:
* `(f_array, f_sp, phi_sp)` if complex transform
* `(f_array, f_sp)` if real transform



## pyssht.inverse

~~~~
f = pyssht.inverse(np.ndarray[ double complex, ndim=1, mode="c"] f_lm not None, L, Spin=0, Method='MW', Reality=False)
~~~~

Performs the inverse spherical harmonic transform.

#### Inputs

* `flm` the spherical harmonic transform of `f`, `numpy.ndarray` type `complex`, ndim 1
* `L` the band limit of the signal, non-zero positive integer
* `Spin` the spin of the signal, non-negative integer (default = 0)
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    2. `'MW_pole'`    [McEwen & Wiaux sampling with the south pole as a seperate double.]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]
* `Reality`  determines if the signal is real or complex, Boolian (default = False)

#### Output

`f` the signal on the sphere, 2D `numpy.ndarray` type `complex` or `real`. NB different for `'MW_pole'` sampling.

#### Note on `'MW_pole'` sampling

This is the same as the `'MW'` sampling however the south pole is expessed as a double only not a vector. Therefore the size of the array is one smaller on the \(\theta\) direction. `f` is now a tuple containing either:
* `(f_array, f_sp, phi_sp)` if complex transform
* `(f_array, f_sp)` if real transform



## pyssht.forward_adjoint

~~~~
f = pyssht.forward_adjoint(np.ndarray[ double complex, ndim=1, mode="c"] f_lm not None, L, Spin=0, Method='MW', Reality=False)
~~~~

Performs the adjoint of the forward spherical harmonic transform.

#### Inputs

* `flm` the spherical harmonic transform of `f`, `numpy.ndarray` type `complex`, ndim 1
* `L` the band limit of the signal, non-zero positive integer
* `Spin` the spin of the signal, non-negative integer (default = 0)
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
* `Reality`  determines if the signal is real or complex, Boolian (default = False)

#### Output

`f` the signal on the sphere, 2D `numpy.ndarray` type `complex` or `real`.


## pyssht.inverse_adjoint

~~~~{.python}
flm = pyssht.inverse_adjoint(f, int L, Spin=0, Method='MW', Reality=False)
~~~~

Performs the adjoint of the inverse spherical harmonic transform.

#### Inputs

* `f` the signal on the sphere, `numpy.ndarray` type `complex` or `real`, ndim 2.
* `L` the band limit of the signal, non-zero positive integer
* `Spin` the spin of the signal, non-negative integer (default = 0)
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
* `Reality`  determines if the signal is real or complex, Boolian (default = False)

#### Output

`flm` the spherical harmonic transform of `f`, 1D `numpy.ndarray` type `complex`


## pyssht.elm2ind

~~~~
index = pyssht.elm2ind( int el, int m)
~~~~

Computes the index in the `flm` array of a particular harmonic coeeficient \(\ell \) and \(m\).

#### Inputs

* `el` the scale parameter of the spherical harmonic coefficients, integer from \(0\) to \(L-1\), where \(L\) is the band limit.
* `em` the azimuthal parameter, integer from -el to el.

#### Output

Index of the coficiant in `flm` array, integer

## pyssht.ind2elm

~~~~
(el, em) = pyssht.ind2elm(int ind)
~~~~

Computes harmonic coeeficient \(\ell \) and \(m\) from the index in the `flm` array.

#### Inputs

* `ind` index of the `flm` array

#### Output

Tuple containing `(el, em)`
* `el` the scale parameter of the spherical harmonic coefficients, integer from \(0\) to \(L-1\), where \(L\) is the band limit.
* `em` the azimuthal parameter, integer from -el to el.

## pyssht.theta_to_index

~~~~
p = pyssht.theta_to_index(double theta, int L, str Method="MW")
~~~~

Outputs the \(\theta\) index (the first) in the 2 demensional array used to store spherical images. The index returned is that of the closest \(\theta\) sample smaller then the angle given on input.

#### Inputs

* `theta` the angle \(\theta\)
* `L` the band limit of the signal, non-zero positive integer
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    2. `'MW_pole'`    [McEwen & Wiaux sampling with the south pole as a seperate double.]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]

#### Output

Int `p` of corresponding to the angle \(\theta\).

## pyssht.phi_to_index

~~~~
q = pyssht.phi_to_index(double phi, int L, str Method="MW")
~~~~

Outputs the \(\phi\) index (the second) in the 2 demensional array used to store spherical images. The index returned is that of the closest \(\phi\) sample smaller then the angle given on input.

#### Inputs

* `phi` the angle \(\phi\)
* `L` the band limit of the signal, non-zero positive integer
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    2. `'MW_pole'`    [McEwen & Wiaux sampling with the south pole as a seperate double.]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]

#### Output

Int `q` of corresponding to the angle \(\phi\).

## pyssht.sample_length

~~~~
n = pyssht.sample_length(int L, Method = 'MW')
~~~~

Outputs a size of the array used for storing the data on the sphere for different sampling schemes.

#### Inputs

* `L` the band limit of the signal, non-zero positive integer
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    2. `'MW_pole'`    [McEwen & Wiaux sampling with the south pole as a seperate double.]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]

#### Output

Int `n` equal to the collapsed 1 dimensional size of the 2 demensional array used to store data on the sphere.

## pyssht.sample_shape

~~~~
(n_theta, n_phi) = pyssht.sample_shape(int L, Method='MW')
~~~~

Outputs a tuple with the shape of the array used for storing the data on the sphere for different sampling schemes.

#### Inputs

* `L` the band limit of the signal, non-zero positive integer
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    2. `'MW_pole'`    [McEwen & Wiaux sampling with the south pole as a seperate double.]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]

#### Output

Tuple containing `(n_theta, n_phi)`
* `n_theta` the number of samples in the \(\theta\) direction, integer
* `n_phi` the number of samples in the \(\phi\) direction, integer


## pyssht.sample_positions

~~~~
(thetas, phis) = pyssht.sample_positions(int L, Method = 'MW', Grid=False)
~~~~

Computes the positions on the sphere of the samples.

#### Inputs

* `L` the band limit of the signal, non-zero positive integer
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    2. `'MW_pole'`    [McEwen & Wiaux sampling with the south pole as a seperate double.]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]
* `Grid` describes if the output is a vector of the smaple positions or a 2D array the same shape as the signal on the sphere, default `False`

#### Outputs

Tuple containing `(thetas, phis)`
* `thetas` positions of the samples in the \(\theta\) direction
* `phis` positions of the samples in the \(\theta\) direction

## pyssht.s2_to_cart

~~~~
(x, y, z) = pyssht.s2_to_cart(theta, phi)
~~~~

Computes the \(x\), \(y\), and \(z\) coordinates from \(\theta\) and \(\phi\) on the sphere.

#### Inputs

* `theta` \(\theta\) values, type `numpy.ndarray`
* `phi` \(\phi\) values, type `numpy.ndarray`

#### Output

Tuple containing `(x, y, z)`
* `x` the \(x\) coordinate of each point, type `numpy.ndarray`
* `y` the \(y\) coordinate of each point, type `numpy.ndarray`
* `z` the \(z\) coordinate of each point, type `numpy.ndarray`

## pyssht.cart_to_s2

~~~~
thetas, phis = cart_to_s2(x, y, z)
~~~~

Computes the \(\theta\) and \(\phi\) on the coordinates on the sphere from \(x\), \(y\), and \(z\) coordinates.

#### Inputs

* `x` \(x\) values, type `numpy.ndarray`
* `y` \(y\) values, type `numpy.ndarray`
* `z` \(z\) values, type `numpy.ndarray`

#### Output

Tuple containing `(theta, phi)`
* `theta` the \(\theta\) coordinate of each point, type `numpy.ndarray`
* `phi` the \(\phi\) coordinate of each point, type `numpy.ndarray`


## pyssht.spherical_to_cart

~~~~
(x, y, z) = pyssht.spherical_to_cart(r, theta, phi)
~~~~

Computes the \(x\), \(y\), and \(z\) coordinates from the sphrical coordinates \(r\), \(\theta\) and \(\phi\).

#### Inputs

* `r` \(r\) values, type `numpy.ndarray`
* `theta` \(\theta\) values, type `numpy.ndarray`
* `phi` \(\phi\) values, type `numpy.ndarray`

#### Output

Tuple containing `(x, y, z)`
* `x` the \(x\) coordinate of each point, type `numpy.ndarray`
* `y` the \(y\) coordinate of each point, type `numpy.ndarray`
* `z` the \(z\) coordinate of each point, type `numpy.ndarray`

## pyssht.cart_to_spherical

~~~~
r, theta, phi = pyssht.cart_to_spherical(x, y, z)
~~~~


Computes the \(\r\), \(\theta\) and \(\phi\) on the sperical coordinates from \(x\), \(y\), and \(z\) coordinates.

#### Inputs

* `x` \(x\) values, type `numpy.ndarray`
* `y` \(y\) values, type `numpy.ndarray`
* `z` \(z\) values, type `numpy.ndarray`

#### Output

Tuple containing `(r, theta, phi)`
* `r` the \(r\) coordinate of each point, type `numpy.ndarray`
* `theta` the \(\theta\) coordinate of each point, type `numpy.ndarray`
* `phi` the \(\phi\) coordinate of each point, type `numpy.ndarray`


## pyssht.theta_phi_to_ra_dec

~~~~
(dec, ra) = pyssht.theta_phi_to_ra_dec(theta, phi, Degrees=False)
~~~~

Computes the Right Assension and declination from an array of \(\theta\) and \(\phi\) values.

#### Inputs

* `theta` \(\theta\) values, type `numpy.ndarray`
* `phi` \(\phi\) values, type `numpy.ndarray`
* `Degrees` defines if the output is in degrees or radians

#### Output

Tuple contaning `(dec, ra)`
* `dec` the declination angle, `numpy.ndarray`
* `ra` the Right Assension, `numpy.ndarray`


## pyssht.ra_dec_to_theta_phi

~~~~
(theta, phi) = pyssht.ra_dec_to_theta_phi(ra, dec, Degrees=False)
~~~~

Computes the \(\theta\) and \(\phi\) values from an array of Right Assension and declination values.

#### Inputs

* `dec` the declination angle, `numpy.ndarray`
* `ra` the Right Assension, `numpy.ndarray`
* `Degrees` defines if the input is in degrees or radians, if degrees they are converted

#### Output

Tuple contaning `(theta, phi])`
* `theta` \(\theta\) values, type `numpy.ndarray`
* `phi` \(\phi\) values, type `numpy.ndarray`

## pyssht.make_rotation_matrix

~~~~
rot_much = pyssht.make_rotation_matrix(list rot)
~~~~

Computes the 3 by 3 rotation matrix from the Eular angles given on input

#### Inputs

* `rot` List of length 3. Each element are the Eular angles `[alpha, beta, gamma]`

#### Output

3 by 3 `rot_matrix` the rotation matrix type `ndarray` dtype `float`

## pyssht.rot_cart

~~~~
x_p, y_p, z_p = pyssht.rot_cart(x, y, z, list rot)
~~~~

Computes the rotations of the cartisian coordinates given a set of Eular angles. The inputs can be any shape `ndarray`s. For speed if the arrays are 1 or 2 demensional it is recommended to use `pyssht.rot_cart_1D` or `pyssht.rot_cart_2D`.

#### Inputs

* `x` \(x\) values, type `numpy.ndarray`
* `y` \(y\) values, type `numpy.ndarray`
* `z` \(z\) values, type `numpy.ndarray`
* `rot` List of length 3. Each element are the Eular angles `[alpha, beta, gamma]`

#### Output

Tuple containing `(x_p, y_p, z_p)` the rotated coordinates the same shape and type as the inputs.

## pyssht.rot_cart_1d and pyssht.rot_cart_1d

~~~~
(x_p, y_p, z_p) = pyssht.rot_cart_1d(np.ndarray[np.float_t, ndim=1] x, np.ndarray[np.float_t, ndim=1] y, np.ndarray[np.float_t, ndim=1] z, list rot)
~~~~

~~~~
(x_p, y_p, z_p) = pyssht.rot_cart_1d(np.ndarray[np.float_t, ndim=2] x, np.ndarray[np.float_t, ndim=2] y, np.ndarray[np.float_t, ndim=2] z, list rot)
~~~~

Computes the rotations of the cartisian coordinates given a set of Eular angles. The inputs can be any shape `ndarray`s. Same as `pyssht.rot_cart` except optimised for arrays that are 1 or 2 demensional.

#### Inputs

* `x` \(x\) values, type `numpy.ndarray`, dtype `float`, ndim 1 or 2
* `y` \(y\) values, type `numpy.ndarray`, dtype `float`, ndim 1 or 2
* `z` \(z\) values, type `numpy.ndarray`, dtype `float`, ndim 1 or 2
* `rot` List of length 3. Each element are the Eular angles `[alpha, beta, gamma]`

#### Output

Tuple containing `(x_p, y_p, z_p)` the rotated coordinates the same shape and type as the inputs.



## pyssht.plot_sphere

~~~~
pyssht.plot_sphere(f, L, Method='MW', Close=True, Parametric=False,\
                    Parametric_Saling=[0.0,0.5], Output_File=None,\
                    Show=True, Color_Bar=True, Units=None, Color_Range=None,\ Axis=True)
~~~~

Plots data on to a sphere. It is really slow and not very good!

#### Inputs

* `f` the signal on the sphere, `numpy.ndarray` type `complex` or `real`, ndim 2. NB different for `'MW_pole'` sampling.
* `L` the band limit of the signal, non-zero positive integer
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    2. `'MW_pole'`    [McEwen & Wiaux sampling with the south pole as a seperate double.]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]
* `Close` if true the full sphere is plotted (without a gap after the last \(\phi\) position), default `True`
* `Parametric` the radius of the object at a certain point is defined by the function (not just the color), default `False`
* `Parametric_Saling` used if `Parametric=True`, defines the radius of the shape at a particular angle `r = norm(f)*Parametric_Saling[1] + Parametric_Saling[0]`, default `[0.0,0.5]`
* `Output_File` if set saves the plot to a file of that name
* `Show` if `True` shows you the plot, default `False`
* `Color_Bar` if `True` shows the color bar, default `True` 
* `Units` is set puts a label on the color bar
* `Color_Range` if set saturates the color bar in that range, else the function min and max is used
* `Axis` if `True` shows the 3d axis, default `True`

#### Outputs

None

## pyssht.mollweide_projection

~~~~
f_plot, mask(, f_plot_imag, mask_imag) = pyssht.mollweide_projection(f, int L,\
                        int resolution=500, rot=None,\
                        zoom_region=[np.sqrt(2.0)*2,np.sqrt(2.0)], str Method="MW")
~~~~

Creates an `ndarray` of the mollweide projection of a spherical image and a mask array. This is usefull for plotting results. Elements in the signal `f` that are `NaN`s are marked in the mask. This allows one to plot these regions the color of their choice.

Here is an example of using the function to plot real spherical data.

~~~~
f_plot, mask = pyssht.mollweide_projection(f, L, Method="MW") # make projection
plt.figure() # start figure
imgplot = plt.imshow(f_real_plot,interpolation='nearest') # plot the projected image
plt.colorbar(imgplot,fraction=0.025, pad=0.04) # plot color bar (these extra keywords make the bar a reasonable size)
plt.imshow(mask_real, interpolation='nearest', cmap=cm.gray, vmin=-1., vmax=1.) # plot the NaN regions in grey
plt.gca().set_aspect("equal") # ensures the region is the correct proportions
plt.axis('off') # removes axis (looks better)
plt.show()
~~~~

#### Inputs

* `f` the signal on the sphere, `numpy.ndarray` type `complex` or `real`, ndim 2.
* `L` the band limit of the signal, non-zero positive integer
* `resolution` size of the projected image, default 500
* `rot` If the image should be rotated before projecting, None. `rot` should be a list of length 1 or 3. If 1 then the image is roated around the \(z\) axis by that amount. If 3 then the image is rotated by the Eular angles given in the list. 
* `zoom_region` the region of the sphere to be ploted, default `[np.sqrt(2.0)*2,np.sqrt(2.0)]` is the full sphere.
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]


#### Outputs

If the input is real:

Tuple containing:
* `f_plot` the projection of the image as a 2 dimensional `ndarray` of type `float`. Masked regions and regions not in the sphere are `NaN`s to make the clear when plotted
* `mask` the projection of the masked regions (`NaN`s in input `f`) as a 2 dimensional `ndarray` of type `float`. Masked regions have a value `0.0` and regions not in the sphere are `NaN`s to make the clear when plotted.

If the input is complex:

Tuple containing:
* `f_plot_real` the projection of the real part of the image as a 2 dimensional `ndarray` of type `float`. Masked regions and regions not in the sphere are `NaN`s to make the clear when plotted
* `mask_real` the projection of the masked regions (`NaN`s in input `f.real`) as a 2 dimensional `ndarray` of type `float`. Masked regions have a value `0.0` and regions not in the sphere are `NaN`s to make the clear when plotted.
* `f_plot_imag` the projection of the imaginary part of the image as a 2 dimensional `ndarray` of type `float`. Masked regions and regions not in the sphere are `NaN`s to make the clear when plotted
* `mask_imag` the projection of the masked regions (`NaN`s in input `f.imag`) as a 2 dimensional `ndarray` of type `float`. Masked regions have a value `0.0` and regions not in the sphere are `NaN`s to make the clear when plotted.

## pyssht.orthographic_projection

~~~~
orth_proj_north_real, mask_north_real, orth_proj_south_real, mask_south_real,\
(orth_proj_north_imag, mask_north_imag, orth_proj_south_imag, mask_south_imag\ )
            = pyssht.orthographic_projection(f, int L, int resolution=500,\
             rot=None, float zoom_region=np.pi/2, str Method="MW")
~~~~

Creates an two `ndarray`s of the orthagraphic projection of a spherical image and a mask array. This is usefull for plotting results. Elements in the signal `f` that are `NaN`s are marked in the mask. This allows one to plot these regions the color of their choice.

Here is an example of using the function to plot real spherical data.

~~~~
orth_proj_north, mask_north, orth_proj_south, mask_south \
        = pyssht.orthographic_projection(k_mw, L, resolution=500, Method="MW")
plt.figure() # start figure
imgplot = plt.imshow(orth_proj_north,interpolation='nearest')# plot the projected image (north part)
plt.colorbar(imgplot) # plot color bar
plt.imshow(mask_north, interpolation='nearest', cmap=cm.gray, vmin=-1., vmax=1.) # plot the NaN regions in grey
plt.axis('off') # removes axis (looks better)

plt.figure()
imgplot = plt.imshow(orth_proj_south,interpolation='nearest')# plot the projected image (south part)
plt.colorbar(imgplot)
plt.imshow(mask_south, interpolation='nearest', cmap=cm.gray, vmin=-1., vmax=1.)
plt.title("orthographic projection south")
plt.axis('off')
plt.show()
~~~~

#### Inputs

* `f` the signal on the sphere, `numpy.ndarray` type `complex` or `real`, ndim 2.
* `L` the band limit of the signal, non-zero positive integer
* `resolution` size of the projected image, default 500
* `rot` If the image should be rotated before projecting, None. `rot` should be a list of length 1 or 3. If 1 then the image is roated around the \(z\) axis by that amount. If 3 then the image is rotated by the Eular angles given in the list. 
* `zoom_region` the region of the sphere to be ploted in radians, default `np.pi/2` is the full half sphere.
* `Method` the sampling scheme used, string:
    1. `'MW'`         [McEwen & Wiaux sampling (default)]
    3. `'MWSS'`       [McEwen & Wiaux symmetric sampling]
    4. `'DH'`         [Driscoll & Healy sampling]
    5. `'GL'`         [Gauss-Legendre sampling]


#### Outputs

If the input is real:

Tuple containing:
* `f_plot_north` the projection of the north part of the image as a 2 dimensional `ndarray` of type `float`. Masked regions and regions not in the sphere are `NaN`s to make the clear when plotted
* `mask_north` the projection of the north part of the masked regions (`NaN`s in input `f`) as a 2 dimensional `ndarray` of type `float`. Masked regions have a value `0.0` and regions not in the sphere are `NaN`s to make the clear when plotted.
* `f_plot_south` the projection of the south part of the image as a 2 dimensional `ndarray` of type `float`. Masked regions and regions not in the sphere are `NaN`s to make the clear when plotted
* `mask_south` the projection of the south part of the masked regions (`NaN`s in input `f`) as a 2 dimensional `ndarray` of type `float`. Masked regions have a value `0.0` and regions not in the sphere are `NaN`s to make the clear when plotted.

If the input is complex:

Tuple containing:
* `f_plot_north_real` the projection of the north part of the real part of the image as a 2 dimensional `ndarray` of type `float`. Masked regions and regions not in the sphere are `NaN`s to make the clear when plotted
* `mask_north_real` the projection of the north part of the real part of the masked regions (`NaN`s in input `f`) as a 2 dimensional `ndarray` of type `float`. Masked regions have a value `0.0` and regions not in the sphere are `NaN`s to make the clear when plotted.
* `f_plot_south_real` the projection of the south part of the real part of the image as a 2 dimensional `ndarray` of type `float`. Masked regions and regions not in the sphere are `NaN`s to make the clear when plotted
* `mask_south_real` the projection of the south part of the real part of the masked regions (`NaN`s in input `f`) as a 2 dimensional `ndarray` of type `float`. Masked regions have a value `0.0` and regions not in the sphere are `NaN`s to make the clear when plotted.
* `f_plot_north_imag` the projection of the north part of the imaginary part of the image as a 2 dimensional `ndarray` of type `float`. Masked regions and regions not in the sphere are `NaN`s to make the clear when plotted
* `mask_north_imag` the projection of the north part of the imaginary part of the masked regions (`NaN`s in input `f`) as a 2 dimensional `ndarray` of type `float`. Masked regions have a value `0.0` and regions not in the sphere are `NaN`s to make the clear when plotted.
* `f_plot_south_imag` the projection of the south part of the imaginary part of the image as a 2 dimensional `ndarray` of type `float`. Masked regions and regions not in the sphere are `NaN`s to make the clear when plotted
* `mask_south_imag` the projection of the south part of the imaginary part of the masked regions (`NaN`s in input `f`) as a 2 dimensional `ndarray` of type `float`. Masked regions have a value `0.0` and regions not in the sphere are `NaN`s to make the clear when plotted.


## pyssht.dl_beta_recurse

~~~~
dl = pyssht.dl_beta_recurse(np.ndarray[ double, ndim=2, mode="c"] dl not None,\
            double beta, int L, int el, \
            np.ndarray[ double, ndim=1, mode="c"] sqrt_tbl not None,\
            np.ndarray[ double, ndim=1, mode="c"] signs not None)
~~~~

Function to recursively calculate the small Wigner D matricies.

Documentation to be added.

## pyssht.generate_dl

~~~~
dl_array = pyssht.generate_dl(double beta, int L)
~~~~

Generates the small Wigner D matricies up to a given band limit for a given \(\beta\)

#### Inputs

* `beta` angle to calculate Wigner D matrix at, type `double`
* `L` the band limit of the signal, non-zero positive integer

#### Outputs

Numpy ndarray `dl_array`, type `float_` of the small Wigner D matricies

## pyssht.rotate_flms

~~~~
flm_rotated = pyssht.rotate_flms(
                np.ndarray[ double complex, ndim=1, mode="c"] f_lm not None,\
                double alpha, double beta, double gamma, int L, dl_array=None,\
                M=None, Axisymmetric=False, Keep_dl=False)
~~~~

Function to rotate a set of spherical harmonic coefficients by the set of Eular angles \(\alpha, \beta, \gamma \) using the \(z,y,z\) convention.

#### Inputs

* `flm` the spherical harmonic transform of `f`, `numpy.ndarray` type `complex`, ndim 1
* `alpha` rotation angle \(\alpha\), type `double`
* `beta` rotation angle \(\beta\), type `double`
* `gamma` rotation angle \(\gamma\), type `double`
* `L` the band limit of the signal, non-zero positive integer
* `dl_array` if set should be the precomuted small Wigner D matirix for angle \(\beta\) and harmonic band limit `L`. If not set this is calculated in the function.
* `M` if set is the azimuthal band limit of the function to be rotated, default `M=L`.
* `Axisymmetric` set if the function is axisymetic and axisytric harmonic coefficients are parsed.
* `Keep_dl` if set the output is changed to allow one to keep the computed `dl_array`

#### Output

If `Keep_dl` is not set the output is the rotated set of spherical harmonic coeficiants. If it is the output is a tuple `(flm_rotated, dl_array)`, ie the rotated harmonic coefficients and the small Wigner D matirix computed for that band limit and \(\alpha\) value.

## pyssht.guassian_smoothing

~~~~
fs_lm = pyssht.guassian_smoothing(np.ndarray[ double complex, ndim=1, mode="c"] f_lm not None, int L, sigma_in=None, bl_in = None)
~~~~

Smooths a set of harmonic coefficients either with a precomputed smoothing kernal `bl` or with a Gaussian given on input.

#### Inputs

* `f_lm` the spherical harmonic transform of `f`, `numpy.ndarray` type `complex`, ndim 1
* `L` the band limit of the signal, non-zero positive integer
* `sigma_in` the input sigma of the Gaussian to smooth the signal with, default `None`
* `bl_in` the smoothing kernal to smooth the signal with, default `None` 

#### Output

* `fs_lm` the smoothed harmonic coefficients.