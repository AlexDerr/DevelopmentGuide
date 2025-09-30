# Makefile

Used for automationm of common tasks at a project level

Documentation: https://www.gnu.org/software/make/manual/make.html

## Examples
Example in MLTE: https://github.com/mlte-team/mlte/blob/master/Makefile

```make
# ~/Makefile

# Declare the target "clean" to be phony
#   https://www.gnu.org/software/make/manual/make.html#Phony-Targets
.PHONY: clean
# Define the target "clean" to call `rm -rf temp`
clean:
    rm -rf temp

# Now, `make clean` will exectute `rm -rf temp`
```