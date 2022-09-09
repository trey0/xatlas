
# example_repack

## Install

Follow the `xatlas` installation instructions as usual. If you only need
the `example_repack` binary, as a shortcut, you can replace `make` with
`make example_repack`.

## Example usage

```bash
mkdir test_fuze
cd test_fuze

# download sample model with extraneous imagery in texture atlas
curl -O https://raw.githubusercontent.com/mikedh/trimesh/main/models/fuze.obj
curl -O https://raw.githubusercontent.com/mikedh/trimesh/main/models/fuze.obj.mtl
curl -O https://raw.githubusercontent.com/mikedh/trimesh/main/models/fuze%20uv.jpg

# fix texture atlas filename because OBJ parser can't handle spaces in filenames
mv "fuze%20uv.jpg" fuze_uv.jpg
sed -i "s/fuze uv.jpg/fuze_uv.jpg/" fuze.obj.mtl

# your path may vary
REPACK="<your_prefix>/xatlas/build/gmake_gcc/bin/Release/x86_64/example_repack"

$REPACK fuze.obj out
# now we should have out.{obj,mtl,jpg} with repacked texture

# optionally compare input to output
ls -lh fuze_uv.jpg out.jpg
identify fuze_uv.jpg out.jpg
meshlab fuze.obj
meshlab out.obj
```
