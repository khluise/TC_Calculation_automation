# Quantum ESPRESSO TC Calculation Workflow Automation

This repository provides a Python script to automate the workflow for superconducting transition temperature (Tc) calculations using Quantum ESPRESSO. The script orchestrates a sequence of calculations involving `pw.x`, `ph.x`, `q2r.x`, `matdyn.x`, and `lambda.x`, handling input preparation, output parsing, and file management for a streamlined, reproducible process.

## Features
- **Interactive Input**: Prompts the user for all necessary parameters, including input files, calculation settings, and smearing methods.
- **Stepwise Automation**: Automates SCF, a2F, phonon, q2r, matdyn (band and DOS), and lambda calculations.
- **Resumable Workflow**: Tracks progress in a log file, allowing interrupted workflows to resume from the last completed step.
- **Output Management**: Organizes outputs in dedicated directories and provides a summary of results.
- **Error Handling**: Detects and reports errors at each step, halting the workflow if a critical issue occurs.
- **Re-run Lambda Calculation**: Allows re-running only the final lambda.x step with a new Coulomb coefficient without repeating the full workflow.

## Requirements
- Python 3.x
- Quantum ESPRESSO executables (`pw.x`, `ph.x`, `q2r.x`, `matdyn.x`, `lambda.x`) available in your `PATH`
- MPI (for parallel execution with `mpirun`)

## Usage
1. **Prepare Input Files**: Ensure your Quantum ESPRESSO input files (e.g., `pb.scf.in`, `elph.in`, `matdyn.in.fre`) are present in the working directory. Example files are provided in the repository.

   **Note:** In the `matdyn.in.fre` file, the q points must be in band form.

   For help in preparing these input files, visit:
   - [INPUT_PW documentation](https://www.quantum-espresso.org/Doc/INPUT_PW.html)
   - [INPUT_PH documentation](https://www.quantum-espresso.org/Doc/INPUT_PH.html)
   - [INPUT_MATDYN documentation](https://www.quantum-espresso.org/Doc/INPUT_MATDYN.html)

2. **Run the Script**:
   ```sh
   ./QE_TC_calulation_workflow.x
   ```
3. **Follow Prompts**: The script will interactively request:
   - Number of CPU cores
   - Paths to input files for `pw.x`, `ph.x`, and `matdyn.x`
   - ZASR value
   - High symmetry points
   - k-point grid and DOS parameters
   - Smearing and degauss values for lambda.x
   - Coulomb coefficient
4. **Workflow Execution**: The script will execute each step, logging progress in `workflow.log`. If interrupted, simply rerun the script to resume.
5. **Re-running Lambda Calculation**: If all steps are complete, you can re-run only the lambda.x calculation with a new Coulomb coefficient.

## Output Files
- `scf_.out`: SCF calculation output
- `scf_a2F.out`: a2F calculation output
- `elph/elph.out`: Phonon calculation output
- `q2r.out`: q2r calculation output
- `matdyn.out.fre` or as specified: matdyn band calculation output
- `matdyn.out.dos`: matdyn DOS calculation output
- `lambda.out`: lambda.x calculation output
- `workflow.log`: Progress and user input log

## Directory Structure
- `scf/`, `scf_a2F/`, `elph/`: Calculation-specific directories for outputs and intermediate files


## Customization
- The script can be modified to suit different input file naming conventions or calculation parameters.
- All user inputs are stored in `workflow.log` for reproducibility.

## Troubleshooting
- If a step fails, check the corresponding output file (e.g., `scf.out`, `elph.out`) for error messages.
- Ensure all Quantum ESPRESSO executables are accessible and input files are correctly formatted.
- For floating-point warnings, the script will attempt to ignore non-critical ones.

## Author
**Luise**  
Email: luisekh076@gmail.com

---
© kh.luise
