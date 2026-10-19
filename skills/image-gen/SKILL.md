---
name: image-gen
description: Generate or edit images with Codex's built-in $imagegen skill. Use for /image-gen or when the user asks to generate or edit an image.
argument-hint: <what to draw>
---

Send the user's request to Codex unchanged (Bash timeout 600000 ms).
If the user gives existing images to edit or use as reference, add --image <absolute path> for each.

codex exec --sandbox read-only --skip-git-repo-check [--image <path>] <<'EOF' 2>/dev/null
$imagegen <user's request>

Reply with the absolute path of each image.
EOF

Check that each returned file exists. If generation failed or a file is missing, report the error and do not retry.

Show every image in chat with SendUserFile (display: render) if available; otherwise give a clickable link to each file.
SendUserFile previews only files inside the session's folders or scratchpad, so first copy each image into your scratchpad directory (if you have one) and send the copy.

Images stay where Codex saved them. Copy them elsewhere only if the user asks for them to be saved or used somewhere (for example on a site or in app); then put them where that use needs them.
