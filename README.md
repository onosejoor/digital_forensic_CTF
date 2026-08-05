# DIGITAL FORENSIC EXAMINATION REPORT

**Case Reference:** CASE-001-04-08-2026-V1  
**Examiner:** Ejoor Onos Henry  
**Agency/Unit:** Digital Forensics Laboratory, Pacestacks Systems  
**Date of Report:** 5 August 2026  
**Evidence Item:** `cartel.img` (USB Storage Device)  
**Date of Acquisition:** 2 August 2026  

---

### 1. Objectives
The purpose of this examination was to identify, preserve, examine, analyse, and document digital evidence contained within the forensic image `cartel.img` recovered during an EFCC search operation. The examination was conducted to determine the nature of data stored on the device and to verify the suspect’s claim that the USB contained only personal photographs.

### 2. Tools Used
- Autopsy 4.23.1  
- FTK Imager 8.2.0  
- WinHex  
- The Sleuth Kit (fls, fsstat, icat, strings)  
- PowerShell (Get-FileHash)  
- PhotoRec (via Autopsy carving module)

### 3. Evidence Verification (Task 1)
Integrity verification was performed prior to any examination:

- **MD5:** `80348C58EEC4C328EF1F7709ADC56A54`  
- **SHA-256:** `CE550424200A997C61B413941C8EF4DF9619A2F96579674952294A176A32BE65`

Integrity verification is a fundamental step in digital forensics. It establishes a baseline cryptographic fingerprint of the evidence. Matching hash values confirm that the image has not been altered during handling or examination, thereby preserving its authenticity and legal admissibility.

### 4. Initial Triage (Task 2)
| Item                    | Finding                          |
|-------------------------|----------------------------------|
| Image Format            | Raw (dd-style)                   |
| File System             | FAT16                            |
| Partition Table         | None (superfloppy layout)        |
| Size                    | 247 MB (259,506,176 bytes)       |
| Volume Serial Number    | 0x4092d9d1                       |
| OEM Name                | mkdosfs                          |
| Cluster Size            | 4096 bytes                       |

These preliminary steps are essential to understand the structure of the storage media, select the correct offset (offset 0), and apply appropriate forensic tools.

### 5. Evidence Discovery & Deleted Data Analysis (Tasks 3 & 4)

**Significant Artifacts Identified:**

1. **gumbo1.txt** (Allocated)  
   - Content: Shrimp and Tasso Gumbo recipe  
   - Timestamps: Created/Written 30 April 2004 18:11:20 UTC  

2. **gumbo2.txt** (Allocated)  
   - Content: Shrimp and Andouille Sausage Gumbo recipe  
   - Timestamps: Created/Written 30 April 2004 18:11:24 UTC  

3. **Seven (7) JPEG Photographs** (Carved from Unallocated Space)  
   - Animal images (alligators/crocodiles, frogs, rhinos)  
   - One image contains embedded copyright metadata: `philg@mit.edu`  
   - Recovery method: File carving (Autopsy PhotoRec & WinHex)

4. **Microsoft Word Document** (Carved)  
   - Carved Name: `f0334472_She_died_in_February_at_the_age_of_74.doc`  
   - Title: She died in February at the age of 74  
   - Author: NO WAY MAN NO WAY MAN NOWAY.  
   - Company: University of New Orleans  
   - Created: 9 August 2005 02:17 UTC  
   - Last Modified: 9 August 2005 02:40 UTC  
   - **Critical Content Excerpt:**  
     > “OK. Things are getting a little weird. I zapped the hard drive and then threw it into the Mississippi River. I’m gonna reformat my USB key after this entry, but try not to destroy the good stuff. I need to change the password on the gnome account that Jeremy gave me. I can probably just do that at Radio Shack.”  
     > “Rhino pictures illegal? Makes me sick. I “hid” the photos...hehehehe.”

5. **Wiping Residue**  
   - Large portions of unallocated space filled with repeating “SORRY.SORRY.SORRY…” pattern, consistent with intentional data overwriting.

**Recovery Methods:**  
Allocated files were extracted using standard file system parsing. Deleted photographs and the Word document were recovered through file carving from unallocated space.

**Data Repository Note:**  
All images and recovered data can be found in the `assets` directory within this repository. The extracted artifacts have been categorically grouped into `images/`, `doc/`, and `text/` folders for review.

### 6. Timeline Reconstruction (Task 5)

| Date / Time (UTC)          | Event                                              |
|----------------------------|----------------------------------------------------|
| 2004-04-30 18:11:20       | Creation of gumbo1.txt                            |
| 2004-04-30 18:11:24       | Creation of gumbo2.txt                            |
| 2005-08-09 02:17:00       | Creation of Word document                         |
| 2005-08-09 02:40:00       | Last modification of Word document                |
| Unknown (post-2005)       | Deletion of photographs and Word document         |
| Unknown                   | Partial wiping of unallocated space (“SORRY” pattern) |

**Limitations:**  
A complete user-activity timeline could not be generated due to limited metadata on carved files and the absence of operating system logs. Additional evidence sources would be required for fuller reconstruction.

### 7. Conclusions
The forensic examination does **not** support the suspect’s statement that the USB device contained only personal photographs.

- The only allocated files present are two cooking recipes.  
- Multiple personal photographs and a detailed personal document were recovered from deleted/unallocated space.  
- The recovered Word document explicitly records the user’s intent to destroy evidence, hide photographs, and reformat the USB device, as well as references to account credentials.

### 8. Recommendations
- Maintain strict chain of custody for the original image.  
- Further analysis of residual data and correlation with other seized evidence is advised.  
- The recovered Word document and photographs should be preserved as key exhibits.

---

**Report prepared by:**  
Ejoor Onos Henry  
Penetration Tester & Digital Forensic Examiner  

**Date:** 5 August 2026
