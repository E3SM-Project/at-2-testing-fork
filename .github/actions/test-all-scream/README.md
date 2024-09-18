# Composite action to call test-all-scream inside a workflow

This action is meant to be used inside a workflow as

  steps:
    ...
    - name: run-test-all-scream
      uses: ./.github/actions/eamxx-test-all-scream
      with:
        build_type: <build-type>
        device: <device>
        run_type: <run-type>

The three parameters have the following valid values:

build_type:
 - sp: single-precision debug build
 - dbg: double-precision debug build
 - fpe: double-precision debug build, with FPE enabled
 - opt: double-precision release build
 - valg: double-precision debug build with valgrind memory check
 - csm: double-precision debug build with cuda compute-sanitizer --tool memcheck
 - csi: double-precision debug build with cuda compute-sanitizer --tool initcheck
 - csr: double-precision debug build with cuda compute-sanitizer --tool racecheck
 - csi: double-precision debug build with cuda compute-sanitizer --tool initcheck

device:
 - openmp: Kokkos::OpenMP backend
 - serial: Kokkos::Serial backend
 - cuda: Kokkos::Cuda backend
 - hip: Kokkos::HIP backend

run_type:
 - nightly: runs tests and then submit to cdash
 - at-run: runs tests without submitting to cdash
 - bless: runs tests and copy output files to baselines folder

All the tests will run with a machine called "ghci-snl-$device". Please, make sure
that you added a machine file ghci-snl-$device.cmake in components/eamxx/cmake/machine-files,
as well as an entry for ghci-snl-$device in components/eamxx/scripts/machine_specs.py.
