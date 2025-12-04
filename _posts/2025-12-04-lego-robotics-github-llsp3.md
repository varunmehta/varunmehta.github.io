---
title: "Show LLSP3 code preview in GitHub"
layout: post
date: 2025-12-04
image: ../assets/images/posts/lego-blockcode.png
headerImage: true
tag:
- robotics
- FLL
- lego
- technical
- architecture
star: false
hidden: false
category: blog
author: varunmehta
description: Extract the SVG from llsp3, and embed in README file.
---

Under the [repository](https://github.com/varunmehta/73461-2025), I've added a simple github workflow file [`extract_svg.yml`](https://github.com/varunmehta/73461-2025/blob/main/.github/workflows/extract-svg.yml) file.

## Extract SVG from LLSP3
The workflow is triggered only when the llsp3 files, in this case under the path `block/PantheraTech.llsp3` is changed 
```
on:
  push:
    paths:
      - 'block/PantheraTech.llsp3'  # Triggers when PantheraTech.llsp3 is pushed
```

Check if `llsp3` file has changed, 
```
      - name: Get changed LLSP3 files
        id: changed-files
        uses: tj-actions/changed-files@v44
        with:
          files: |
            block/PantheraTech.llsp3
```

Extract the svg file from the `llsp3` (`zip`) file
```
      - name: Extract SVG from LLSP3
        if: steps.changed-files.outputs.any_changed == 'true'
        run: |
          file="block/PantheraTech.llsp3"
          echo "Processing: $file"
          
          # LLSP3 files are typically ZIP archives
          # Create a temporary directory for extraction
          temp_dir=$(mktemp -d)
          
          # Extract the LLSP3 file
          unzip -q "$file" -d "$temp_dir" || {
            echo "Failed to extract $file"
            exit 1
          }
          
          # Look for icon.svg in the extracted contents
          svg_file=$(find "$temp_dir" -name "icon.svg" -type f | head -n 1)
          
          if [ -n "$svg_file" ]; then
            echo "Found icon.svg: $svg_file"
            
            # Copy to block/PantheraTech.svg
            cp "$svg_file" "block/PantheraTech.svg"
            echo "Copied SVG to: block/PantheraTech.svg"
          else
            echo "No icon.svg file found in $file"
            exit 1
          fi
          
          # Clean up temp directory
          rm -rf "$temp_dir"
```

The extracted svg file is then committed back to the repository. For `github-actions[bot]` to commit changes, you need to enable **Workflow Permissions**, read more below about it.    
```
      - name: Commit and push changes
        if: steps.changed-files.outputs.any_changed == 'true'
        run: |
          git config --local user.email "github-actions[bot]@users.noreply.github.com"
          git config --local user.name "github-actions[bot]"
          
          git add block/PantheraTech.svg
          
          # Check if there are changes to commit
          if git diff --staged --quiet; then
            echo "No changes to PantheraTech.svg"
          else
            git commit -m "Extract icon.svg from PantheraTech.llsp3 as PantheraTech.svg"
            git push
          fi
```

### Enable permissions for automation
For the `github-actions[bot]` to commit changes back to the repo, you need to enable additional permissions. Follow the steps below

 * Go to your repo's settings
 * Click on the 'Actions' category on the left side that is under 'Code and automation' 
 * Scroll down to 'Workflow permissions' 
 * Select 'Read and write permissions'
 * Click 'Allow Github Actions to create and approve pull requests'
 * Click 'Save.'

### One potential issue
The only drawback with this workflow is when the users try to commit the new file, they need to do a pull before they commit changes even though they are the single machine commit (all kids work off the same machine)

## Display svg on `README.md`
Under the `README.md`, the SVG file is embedded as a regular image file.
```
![/block/PantheraTech.svg](/block/PantheraTech.svg?raw=true)
```

Feel free to copy `extract_svg.yml` and fit it for your repo.