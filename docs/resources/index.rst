.. _resources:

=========
Resources
=========

For the moment this folder hosts only one configuration file, ``config.yaml``.

In the following we report an example:

.. code-block:: yaml

  # Example configuration file for PYIRF

  # Based on protopipe one, it should progressively use GADF nomenclature.

  general:
    # part of the DL2 filename(s) common between particle types
    template_input_file: '{}_onSource.S.3HB9-FD_ID0.eff-0-CUT0'
     # Output table name
    output_table_name: 'table_best_cutoff'
     # where is the DL2 data
    indir: '/Users/michele/Applications/ctasoft/tests/pyirf/EventDisplay/DL2/Paranal_20deg/CUT0'
    # where to store DL3 data
    outdir: '/Users/michele/Applications/ctasoft/tests/pyirf/EventDisplay/from_pyirf'

  analysis:

   # Theta square cut optimisation (opti, fixed, r68)
   thsq_opt:
    type: 'r68'
    value: 0.2  # In degree, necessary for type fixed

   # Normalisation between ON and OFF regions
   alpha: 0.2

   # Minimimal significance
   min_sigma: 5

   # Minimal number of gamma-ray-like
   min_excess: 10

   # Minimal fraction of background events for excess comparison
   bkg_syst: 0.05

   # Reco energy binning
   ereco_binning:  # TeV
    emin: 0.05
    emax: 50
    nbin: 21

   # Reco energy binning
   etrue_binning:  # TeV
    emin: 0.05
    emax: 50
    nbin: 42

  # =============================================================================
  #                               TO REVIEW
  # =============================================================================

  particle_information:
   gamma:
    n_events_per_file: 22500000  #  10**5 * 10
    n_files: 1
    e_min: 0.05
    e_max: 50
    gen_radius: 1000
    diff_cone: 0
    gen_gamma: 2

   proton:
    n_events_per_file: 3750000000  #  2 * 10**5 * 20
    n_files: 1
    e_min: 0.01
    e_max: 100
    gen_radius: 2500
    diff_cone: 1
    gen_gamma: 2
    offset_cut: 1.

   electron:
    n_events_per_file: 450000000  #  10**5 * 20
    n_files: 1
    e_min: 0.005
    e_max: 5
    gen_radius: 1000
    diff_cone: 1
    gen_gamma: 2
    offset_cut: 1.

  # =============================================================================
  # PLEASE, COMPILE THE FOLLOWING PART DEPENDING ON THE CONTENT OF YOUR DL2 FILES
  #
  #           some quantity are mandatory, some optional, some custom
  #
  #           Definitions for mandatory and optional quantities come from
  #           the latest version of GADF.
  #           Custom are there only for legacy data.
  #
  # =============================================================================

  column_definition:

    # MANDATORY COLUMNS

    # Event identification number
    EVENT_ID: 'EVENT_ID'
    # Event time
    TIME: 'TIME'
    # Reconstructed event Right Ascension
    RA: 'RA'
    # Reconstructed event Declination
    DEC: 'DEC'
    # Reconstructed event energy
    ENERGY: 'ENERGY'

    # OPTIONAL COLUMNS
    # Event quality partition
    EVENT_TYPE: 'GH_MVA'
    # Telescope multiplicity. Number of telescopes that have seen the event.
    MULTIP: 'MULTIP'
    # Reconstructed event Galactic longitude
    GLON: 'GLON'
    # Reconstructed event Galactic latitude
    GLAT: 'GLAT'
    # Reconstructed altitude
    ALT: 'ALT'
    # Reconstructed azimuth
    AZ: 'AZ'
    # ecc...to be integrated later


    # COSTUM COLUMNS
    # Observation identification number
    OBS_ID: 'OBS_ID'
    # True energy
    TRUE_ENERGY: 'MC_ENERGY'
    # True altitude
    TRUE_ALT: 'MC_ALT'
    # True azimuth
    TRUE_AZ: 'MC_AZ'
    # Column name for classification output (protopipe)
    classification_output:
      name: 'gammaness' # should be substituted by EVENT_TYPE
      range: [0, 1] # technically always true (some algorithms could have different domains?)
    angular_distance_to_the_src: 'THETA' # WARNING: for point-source simulations!
