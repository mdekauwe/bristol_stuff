## 12th April 2022

To compile on bristol (BlueCrystal), the netcdf libs are not built with intel so we need to use gfortran.

You need to add this to CABLE's build.ksh

host_bc4l()
{
    export NCDIR='/mnt/storage/software/libraries/gnu/netcdf-4.7.3/lib'
    export NCMOD='/mnt/storage/software/libraries/gnu/netcdf-4.7.3/include'
    export FC=gfortran
    export CFLAGS='-O2'
    export LD='-lnetcdf -lnetcdff'
    export LDFLAGS='-L/mnt/storage/software/libraries/gnu/netcdf-4.7.3/lib -O2'
    build_build
    cd ../
    build_status
}

There is also a conflict in the loaded modules (I think related to the anaconda stuff), so:

$ module purge
$ module add libs/netcdf/4.7.3

*Only* load these, the netcdf one also loads gfortran. This works for single processor compiles...
