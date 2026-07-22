# Blueprint Design Instructions

Before diving into the instructions, this tutorial is quite helpful: 
https://youtu.be/Oy9GVEavPqc?si=QhyHjZq0tyU8WPEO

## Creating a Blueprint from a Design
To generate a blueprint from your existing 3D model:
1. In the top-left corner of the workspace, click the **Design** dropdown menu.
2. Navigate down to **Drawing** and select **From Design**.
3. Save your file if prompted. A dialog box will appear where you can select your assembly, choose your template, set the standard (ISO), and pick your sheet size.
4. Click **OK** to generate the drawing canvas, where you can place your base views and start dimensioning. 

## Editing the Bottom Right Legend (Title Block)
The legend at the bottom right corner is crucial for tracking our documentation. Double-click the title block to edit the text attributes. 

<img width="832" height="248" alt="Screenshot 2026-07-22 122441" src="https://github.com/user-attachments/assets/60e3f640-f2d2-42e5-8d95-1b86d1fe35a4" />


Here is exactly what should be written in every section, using our landing platform as an example:
*   **Dept.:** Your sub-team name (e.g., `DRONE`).
*   **Technical reference:** The broader system or document this links to (e.g., `LANDING PLATFORM SPECS`).
*   **Created by:** Our team identifier (e.g., `UCU SPACE ROBOTICS`).
*   **Approved by:** The name of the reviewer (e.g., `Andriy Ozhovych`).
*   **Document type:** What the blueprint depicts (e.g., `Assembly Drawing` or `Part Drawing`).
*   **Document status:** The current phase of the design (`Draft`, `In Review`, `Approved`, or `Released for Manufacturing`).
*   **Title:** The specific name of the part or assembly (e.g., `LANDING PLATFORM`).
*   **DWG No.:** Our standardized drawing number, which should first be the abbreviation of the department and then its number (e.g., `DRN-01`).
*   **Rev.:** The revision tracking number (e.g., `01`).
*   **Date of issue:** The date the document was finalized (e.g., `21/07/2026`).
*   **Sheet:** The current page and total pages (e.g., `1/1`).

*Note: The default "Creation Date" and "Approval Date" fields can be deleted entirely to keep the block looking clean.*

**Adjusting Box Dimensions:**
The dimensions of the boxes can be adjusted depending on the text size. If a title is too long and overlaps the lines, right-click the title block, select "Edit Title Block," and drag the grid lines to ensure the text has plenty of free space. 

## Adding the Team Logo
Make sure to place our graphic in the large empty box on the left side of the legend. You can download the high-resolution logo from this link:
https://drive.google.com/drive/folders/1a09cyxSmIqpz4mxjaWiBsFsWbKJ8whKc

## Final Blueprint Checklist
Before finishing the blueprint and exporting the PDF, please check the following:
- [ ] Are all necessary dimensions (lengths, radii, thread notes) clearly marked without cluttering the page?
- [ ] Are hidden lines toggled on where necessary to show internal geometry?
- [ ] Is the title block completely filled out with the correct DWG No. and Revision?
- [ ] Are the title block boxes properly sized so no text overlaps the borders?
- [ ] Is the team logo inserted, scaled properly, and centered in its box?
- [ ] Did you delete any redundant fields (like Creation/Approval dates) to clean up the legend?
