# BOOK MY SHOW

## Requirements

### Functional Requirements

- User can view event details, show timings, venue and available seat/ticket categories.
- User can select seats/ticket quantity and place a booking.
- User can search for events based on Artist, Event Name, Location.
- User can like the events and will receive notification when that event's tickets are available.
- User can manage their bookings like see their tickets.
- User can pay for the booking.
- User should receive booking confirmation/ticket.

### Non-Functional Requirements

- booking/search should remain available even during high-demand events.
- seat inventory must be strongly consistent enough to avoid double booking.
- search and event pages should respond quickly.
- confirmed bookings/payments must not be lost.
- Should handle huge traffic spikes when popular events go on sale.
- payment/booking flow should tolerate retries/failures safely.

### Scale Estimation

- Average Search QPS = 10000000 * 5  / 100000 = 500 Searches/s
- Peak Seach QPS = 5000 Searches/s
- Average Booking = 10 Bookings/s
- Sustained Peek Booking = 100 Bookings/s
- Flash Sale Peek Booking = 4000 Bookings/s

## APIs Design

- Get Event Details
    GET /v1/event/{eventId}

- Get Tickets
    GET /v1/ticket/{showId}

- Search Events
    GET /v1/search/text={text}&location={location}&type={type}&limit=20

- Book Tickets
  - Reserve Ticket
        POST /v1/booking/reserve
        {
            header : {
                JWT session Token,
                requestId
                },
            body : {List<ticketId>}
        }
        RESPONSE
        {
            body: {
                status,
                reservationId,
                expireTime
            }
        }

  - Confirm Ticket
        POST /v1/booking/confirm
        {
            header : {
                JWT Token,
                reservationId
            }
            body : {payment details}
        }
        RESPONSE
        {
            body : {
                status,
                bookingId
            }
        }

