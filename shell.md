# Find gunzip files and search inside them (-i for case insensitive)

    find ./ -name "*.gz" | xargs zgrep -i "error"