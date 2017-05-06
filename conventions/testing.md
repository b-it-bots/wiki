# Testing and Linting in ROS
## Running `roslint` with catkin
Before merging into the main repository `roslint` is ran on all merge requests. Unless all errors are resolved the merge request will be rejected. To test if your changes would pass the `roslint` test locally:
- Add the following lines to your `CMakelists.txt`:

```CMake
roslint_python()  # pep8 linting
roslint_cpp()     # ROS wrapper of Google's cpplint
```
- Build target `roslint`:
  - with `catkin_make`: `catkin_make roslint_<package_name>`
  - with `catkin_tools`: `catkin build --no-deps <package_name> --make-args roslint`
- If build fail copy and execute the gray line that looks something like the following to see more detailed errors:
```
cd <package_source_directory>; catkin build --get-env <package_name> | catkin env -si  /usr/bin/make roslint --jobserver-fds=6,7 -j; cd -
```
## Running Unit Tests
```bash
catkin run_tests --this --no-deps
```