# mmono

mmono is an overengineered mono hangboard pickup for climbing.

## Dimensions

<img width="3668" height="2884" alt="Screenshot 2025-10-05 at 6 29 35 PM" src="https://github.com/user-attachments/assets/5597e96b-52b6-4659-b957-9eba6fe262b5" />

<img src="https://github.com/user-attachments/assets/c39d3a4a-4358-43b5-bdd5-5bace4f8c19c" />

## Design

This project asks: What is a 20 mm edge?

For a 90° angle, it’s simple.

For a perfect 90° angle, it’s simple—the distance (shown in red) is exactly 20 mm.

<img width="512" height="512" alt="Untitled" src="https://github.com/user-attachments/assets/3398384a-dc8a-4811-bdb5-2176c8588c8d" />

But a 90° edge is harsh on the skin. Sharp edges concentrate stress at a single point, increasing pain and the chance of skin splitting. That’s why all popular hangboards have rounded edges, called fillets in CAD.

<img width="512" height="512" alt="edge fillet" src="https://github.com/user-attachments/assets/279dc64d-3f09-49bb-b1bd-50eb40e3fb96" />

> An edge fillet is a smooth, curved surface with a constant radius that rounds off a sharp corner or transition between two intersecting faces.

Fillets are usually described by their edge radius—the larger the radius, the rounder the edge.

<img width="512" height="512" alt="edgefillet" src="https://github.com/user-attachments/assets/bc7d4cd9-f048-4b06-8794-05052caf1db6" />

Unfortunately, there is no universal fillet radius for hangboards. Different brands use different edge radii:

| Brand / Board | Edge Depth | Edge Radius         | Source |
|---------------|------------|----------------------|--------|
| **Tension**   | 10 mm      | 3.175 mm (≈ 1/8")    | [Tension Climbing](https://tensionclimbing.com/pages/hangboards) |
| **Beastmaker**| 10 mm      | 8 mm                 | [Test4Climbing](https://test4climbing.com/equipment-needed) |
| **Lattice**   | 10 mm      | 10 mm                | [Climbing.com](https://www.climbing.com/skills/training/tom-randalls-guide-to-better-hangboarding-part-1/) |

> Note: More data would be great—this information is hard to find.

Where there is a fillet, the effective edge depth changes. What counts as “correct” depth (red lines)?

This might sound negligible, but for climbers, millimeters matter.

<img width="512" height="512" alt="20mm?" src="https://github.com/user-attachments/assets/45418436-d21e-4cf9-a793-9c0d2cd5a552" />

To objectively define a true edge depth, we must agree on some definitions:

- Total Depth: The total depth, ignoring edge radius. (90° diagram)
- Edge Radius: The measurement of a curved edge
- Effective Length: The usable length along its surface.
- Ineffective Length: The unusable length along its surface.
- Effective Depth: The usable depth of the edge.

Since there's no standard definition of Effective Length and Depth, the goal is propose a mathmatically okish definition.

For a 90° angle, it’s simple. The red line is the usable edge. Your fingers hang there. The blue line is the unusable edge. Your fingers cannot hang there.

<img width="512" height="512" alt="infcc" src="https://github.com/user-attachments/assets/1e44ba31-5094-45d7-ab1b-8c75333042f4" />

For a perfect right angle, the tangent of the corner is undefined, but if there's a small radius (0.01 mm), the tangent gradually transitions from horizontal to vertical, with the midway point at 45°. 

<img width="512" height="512" alt="45" src="https://github.com/user-attachments/assets/9680e3ed-768c-46f0-bcdc-8d5a6fec6073" />

Based on this, we can define the Effective Length as the distance along the edge up to this midway point of the fillet.

<img width="512" height="512" alt="eff45" src="https://github.com/user-attachments/assets/5402707e-150f-4ba5-a0ba-c5e89b541ede" />

Now that Effective Length is defined, we can calculate Effective Depth.

<img width="512" height="512" alt="effectiveDepth" src="https://github.com/user-attachments/assets/0a327fa4-948a-4794-90ec-89df3ceb442a" />

Use the unit circle as a reference

<img width="512" height="1835" alt="Unit-circle" src="https://github.com/user-attachments/assets/3fccecff-cd92-4512-89cb-31054e01ee8e" />

Given Edge Radius & Effective Depth, calculate Total Depth

```
Set edge_radius (blue) =  8mm
Set effective_depth (dotted) = 20mm

Solve for total_depth (green)

red_line = cos(45) * 8mm
pink_line = edge_radius - red_line

total_depth = effective_depth + pink_line
green = dotted + pink
```

<img width="512" height="512" alt="fff" src="https://github.com/user-attachments/assets/df3e8c50-2f41-404b-9bdf-484f69bc2153" />

There are a few ways to calculate:

```
total_depth = effective_depth + (edge_radius * (1 - cos(45))

total_depth = effective_depth + (edge_radius * (1 - 0.5 ** 0.5))
```

Code

```python
import math

effective_depth = 20

edge_radius = 8

total_depth = effective_depth + (edge_radius * (1 - 0.5 ** 0.5))

print(total_depth)
# total_depth = 22.34314575050762
```

Finally, use calculated Total Depth to extrude your mono with a Fillet Radius.

<img width="3580" height="2796" alt="Screenshot 2025-10-05 at 6 21 16 PM" src="https://github.com/user-attachments/assets/74177d5f-b1e8-4e18-a40b-b5c21789626b" />

<img width="3668" height="2884" alt="Screenshot 2025-10-05 at 6 24 33 PM" src="https://github.com/user-attachments/assets/502f97b1-1561-4cff-884c-abe4b585ae7c" />

Conclusion: This looks like an avocdaco 🥑
