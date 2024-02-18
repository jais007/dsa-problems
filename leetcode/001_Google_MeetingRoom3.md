```java
class Room{
    int endTime;
    int roomNo;
    Room(int endTime, int roomNo){
        this.endTime = endTime;
        this.roomNo = roomNo;
    }
}
class Solution {
    public static int mostBooked(int n, int[][] meetings) {
        Arrays.sort(meetings, (a,b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
        int[] count = new int[n];
        PriorityQueue<Integer> freeRooms = new PriorityQueue<>();
        PriorityQueue<Room> busyRooms = new PriorityQueue<>((a, b) -> a.endTime == b.endTime ? a.roomNo - b.roomNo : a.endTime - b.endTime);
        //add freeRooms 
        for (int i = 0; i < n; i++) 
            freeRooms.add(i);

        for (int i = 0; i < meetings.length; i++) {
            int start = meetings[i][0];
            int end = meetings[i][1];

            //check if any busyRooms meeting has been over?
            while(!busyRooms.isEmpty() && busyRooms.peek().endTime <= start){
                Room newAvailableRoom = busyRooms.poll();
                freeRooms.add(newAvailableRoom.roomNo);
            }

            //check if freeRooms available?
            if(!freeRooms.isEmpty()){
                int room = freeRooms.poll();
                busyRooms.offer(new Room(end, room));
                count[room]++;
            }else{
                //if no room is avaible for next meeting
                Room ongoingMeeting = busyRooms.poll();
                end = end + ongoingMeeting.endTime - start;
                busyRooms.offer(new Room(end, ongoingMeeting.roomNo));
                count[ongoingMeeting.roomNo]++;
            }

        }
        int maxBooked = 0;
        int roomWithMaxBooking = 0;
        for(int i=0;i<n;i++){
            if(count[i] > maxBooked){
                maxBooked = count[i];
                roomWithMaxBooking = i;
            }
        }
        return roomWithMaxBooking;
           
    }
```
