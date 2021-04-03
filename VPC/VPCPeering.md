VPCPeering is a means to connect 2 VPC's with each other.

# Charateristic
- The CIDR in both the VPC should not overlap(Connection might end up in loop if overlapped)
- VPC Peering is not transitive.(if VPC[A] -> VPC[B] and VPC[B] -> VPC[C] then it does not mean VPC[A] -> VPC[A]. You will have to make  a separate connection b/w VPC[A] -> VPC[C])