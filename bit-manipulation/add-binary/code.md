### Code

    class Solution {
    public String addBinary(String a, String b) {
        StringBuilder itogRev = new StringBuilder();
        int sizeA = a.length();
        int sizeB = b.length();
        String deltaSting = null;
        int sizeAB = sizeA;
        if(sizeA < sizeB) {
            deltaSting = b.substring(0, sizeB-sizeA);
        }
        else if (sizeB < sizeA) {
            deltaSting = a.substring(0, sizeA-sizeB);
            sizeAB = sizeB;
        }

        byte grade = 0;
        for (int i=1; i<=sizeAB; i++) {
            byte aByte = Byte.parseByte(a.substring(sizeA-i, sizeA-i+1));
            byte bByte = Byte.parseByte(b.substring(sizeB-i, sizeB-i+1));
            itogRev.append(aByte^bByte^grade);
            if(aByte + bByte + grade >1)
                grade = 1;
            else
                grade = 0;
        }

        if (deltaSting != null) {
            int sizeDelta = deltaSting.length();
            if (grade == 1) {
                for (int i = sizeDelta - 1; i >= 0; i--) {
                    byte dByte = Byte.parseByte(deltaSting.substring(i, i + 1));
                    itogRev.append(dByte ^ grade);
                    sizeDelta--;
                    if (dByte == 0) {
                        grade = 0;
                        break;
                    }
                }
            }
            for (int i = sizeDelta - 1; i >= 0; i--) {
                itogRev.append(deltaSting, i, i + 1);
            }
        }

        if (grade == 1) {
            itogRev.append(1);
        }

        return itogRev.reverse().toString();
    }
}

### Notice
Самое простое решене:
Integer.toBinaryString(Integer.parseInt(a, 2) + Integer.parseInt(b, 2));
