# Biomedicalfluid dynamics with a particular focus on cerebral blood flow - Gemini code
Here is a brief description of the project 

The following is a useful reference document for users of the code in project Gemini. This is a project looking to model the various scenarios of acute ischaemic stroke in a virtual population of patients, with the overarching goal of running an ’in silico’ or ’virtual’ clinical trial, which will be eventually accessible to medical professionals.
The primary solution strategy is the finite element method. The open source software FEniCSx is used as a convenient and effective finite element solver for the partial differential equations modelling acute ischaemic stroke. At time of writing the latest version of FEniCSx is from October 2024, that is FEniCSx (0.9). FEniCSx is an evolution of the previous version FEniCS Legacy - this document will describe some aspects of this translation. FEniCSx is comprised of the libraries UFL, Basix, FFCx, and DOLFINx, which are also available on Github. Some improvements on the legacy version include a wide range of available cell types and elements, memory parallelisation, and complex number support.

This repository contains software corresponding to WP5 of the INSIST project (https://www.insist-h2020.eu/).
## Overview
This section should provude a high-level overview of the project's purpose and goals

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Structure](#structure)
- [Contribution](#contribution)
- [License](#license)

## Installation
To install this project, run the following command
Provide examples of how to install and use the project 

## Structure 
Folders: 
- [perfusion](#perfusion)
- [oxygen](#oxygen)
- [sensitivity](#sensitivity)
- [tissue_health](#tissue_health)

Files: 
| Function | Description | 
|----------|----------|
| .dockerignore | |
| .gitignore | |
| .gitlab-ci.vml | |
| API.py | |
| Dockerfile | |
| LICENSE | |
| README.md | |
| VP_mesh_prep.py | |
| brain_meshes.tar.xz | |
| build_and_run_docker_image_sh | |
| cleaner.sh | |
| coupled_perfusion_runner.sh | |
| documentation.pdf | | 
| documentation.tex | | 
| perfusion_runner.sh | |
| perfusion_runner_mod_geom.sh | | 
| requirements.txt | It is the version requirements for each library. |
| runner.py | |
| singularity.def | |
| test_patient.yml | |


### Sensitivity 
#### Overview
- [IO_fcts.py](#IO_fcts.py): ...
- clear.sh
- [comp_infearcted_volume.py](#comp_infarcted_volume.py): ...
- [finite_element_fcts.py](#finite_element_fcts.py): ...
- [infarct_calculation.py](#infarct_calulation.py): ...
- [param_mapping_runner.py](#param_mapping_runner.py): ...
- [perfusion_parameter_sampling.py](#perfusion_parameter_sampling.py): ...
- [plot_sensitivity_results.py](#plot_sensitivity_results.py): ...
- sensitivity.sh
- [suppl_fcts.py](#suppl_fcts.py): ...
### IO_fcts.py
|Function|Input | Output | Description | 
|----------|----------|----------|----------|
| mesh_reader    | mesh_file   | mesh, subdomains, boundaries   | This function is useful for loading mesh data and its regions in parallel computing environments |
| argument_reader    | parser   | parser   | This function is part of a script that processes command-line arguments |
| perm_init_config_reader    | input_file_path   | mesh_file, e_ref, K1_form, res_fldr, save_subres | This function is designed to read and parse an XML configuration file related to permeability initialisation in a finite element simulation. (extract input parameters, ensure numerical data correctly formatted) |
| basic_flow_config_reader | input_file_path | mesh_file, read_inlet_boundary, inlet_boudary_file, inlet_BC_type, permeability_folder, p_arterial, p_venous, K1gm_ref, K2gm_ref, K3gm_ref, gmowm_perm_rat, beat12gm, betagm, gmowm_beta_rat, fe_degr, res_fldr, save_pvd, comp_ave |  |
| basic_flow_config_reader2 | input_file_path, parser | configs | |
| input_file_reader | input_file_path | mesh_file, p_arterial, p_venous, e_ref, K1_ref, K2_ref, K3_ref, beta, fe_degr, res_fldr, pial_surf_file, inflow_file | |
| inlet_file_reader | inlet_boundary_file | boundary_data | |
| initialise_permeabilities | K1_space, K2_space, mesh, permeability_folder | K1, K2,K1.copy(deepcopy=True) | |
| pvd_saver | variable, folder, name | | |
| hdf5_saver | mesh, variable, folder, file_name, variable_name | | |
| hdf5_reader | mesh, variable, folder, file_name, variable_name | | |

Class: dict2obj(dict) 
-> function: _init_ 

### comp_infarcted_volume.py
>Description: 

### finite_element_fcts.py
| Function | Input | Output | Description | 
|----------|----------|----------|----------|
| mesh_reader | mesh_file | mesh, subdomains, boundaries | |
|alloc_fct_spaces | mesh, fe_f=degr | Vp, Vvel, v_1, v_2, v_3, p, p_1, p_2,p_3, K1_space, K2_space ||
|set_up_fe_solver | mesh, V, v_1, v_2, v_3, p, p_1, p_2, p_3, K1, K2, K3, beta12, beta13, beat 21, beta23, beta31, beta 32, boundaries, pa, pv, subdomains, inflow,_file | LHS, RHS, sigma1, sigma2, sigma3, b1, b2, b3, arteriolesboundnary, venulesboundary, boundaryids | |
| set_up_fe_solver2 | mesh, subdomains, boundaries, V, v_1, v_2, v_3, p, p_1, p_2, p_3, K1, K2, K3, beta12, beta23, pa, pv, read_inlet_boundary, inlet_boundary_file, inlet_BC_type | LHS, RHS, sigma1, sigma2, sigma3, BCs | |
| solve_lin_sys | Vp, LHs, RHS, BCs, lin_solver, precond, rtcol, mon_cinv, init_sol | p | |

### infarct_calulation.py
>Description: ....

### param_mapping_runner.py
>Description: ...
### perfusion_parameter_sampling.py
>Description: ...
### plot_sensitivity_results.py
>Description: ...
### suppl_fcts.py
| Function | Input | Output | Description | 
|----------|----------|----------|----------|
| set_coupling_coeff | beta | beta12, beta13, beta21, beta23, beta31, beta32 | |
| comp_vessel_orientation| subdomains, boundaries, mesh, res_fldr, save_subres | e, main_direction | |
| perm_tens_comp | K_space, subdomains, mesh, e_ref, e_loc, K1_form | K1 | |
| scale_permeabilities | subdomains, K1, K2, K3, K1_ref_gm, K2_ref_gm, K2_km_ref_gm, gmowm_prem_rat, res_fldr, save_pvd | K1, K2, K3 | |
| scale_coupling_coefficients | subdomains, beta12gm, beta23gm, gmowm_beta_rat, K2_space, res_fldr, save_pvd | beta12, beta23 | |
| comp_transf_mat| e0, e1 | T | |
| perm_tens_comp_old | K_space, subdomains, mesh, e0, K1_ref, K2_ref, K3_ref, pial_surf_file | K1, K2, K3 | |
| surface_ave | mesh, boundaries, vels, ps | np.array(fluxes), np.array(surf_p_values) | |
| infarct_vol | mesh, subdomains, infarct | np.array(vol_p_values) | |
| perfusion_vol | mesh, subdomains, perfusion | np.array(vol_p_values) | |
| vol_ave | mesh, subdomains, ps, vels | np.array(vol_p_values), np.array(vol_vel_values) | |
| region_label_assembler | region | reion_labels, n_labels | |
