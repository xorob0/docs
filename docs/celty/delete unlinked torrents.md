`find . -type f -links 1 -print | grep mkv | rev | cut -d"/" -f2- | rev | xargs  --no-run-if-empty  rm -rf`
will find all  mkv files not hardlinked and remove the folder they are in