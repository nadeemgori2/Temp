import { JsonController, Get, Req, Res } from 'routing-controllers';
import { ParticipantService } from '../services/ParticipantService';
import { Request, Response } from 'express';

@JsonController('/v1/participants')
export class ParticipantController {
    constructor(private participantService: ParticipantService) {}

    @Get('/')
    public async getParticipants(@Req() req: Request, @Res() res: Response) {
        try {
            const participants = await this.participantService.fetchParticipants();
            return res.status(200).json(participants);
        } catch (error) {
            console.error('Error fetching participants:', error);
            return res.status(500).json({ error: 'Internal Server Error' });
        }
    }
}

import { Service } from 'typedi';


@Service()
export class ParticipantService {
    public async fetchParticipants() {
        // Replace this with actual logic to fetch participants from DB or API
        const mockParticipants = [
            {
                organizationId: '123',
                status: 'Active',
                organizationName: 'Sample Organization',
                createdOn: '2023-01-01',
                legalEntityName: 'Sample Entity',
                countryOfRegistration: 'US',
                companyRegistration: 'ABC123',
                registrationNumber: '123456',
                addressLine1: '123 Main St',
                city: 'New York',
                postcode: '10001',
                country: 'USA',
                requiresParticipantTermsAndConditionsSigning: true,
                logoUri: 'https://example.com/logo.png',
            },
        ];
        return { participants: mockParticipants };
    }
}
